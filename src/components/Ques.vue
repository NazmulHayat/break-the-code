<template>
  <div class="body">
    <div class="mein pa-3 pa-sm-5">
      <v-row dense>
        <v-col class="pinit">
          <Timer 
          :endTime="endTime"
          class="init 
          text-h5
          text-md-h4
          " />
        </v-col>
        <v-spacer></v-spacer>
        <v-col class="last">
          <div class="d-flex pb-1">
            <v-btn
              fab
              color="transparent"
              elevation="1"
              class="mdibtn"
              @click="back()"
              ><v-icon class="mdicon"> mdi-chevron-left</v-icon></v-btn
            >
            <v-btn
              fab
              color="transparent"
              elevation="1"
              class="mdibtn"
              @click="next()"
              ><v-icon class="mdicon"> mdi-chevron-right </v-icon></v-btn
            >
          </div>
        </v-col>
      </v-row>

      <div class="line"></div>
      <v-carousel
        class="carou"
        hide-delimiters
        :show-arrows="false"
        height=""
        v-model="ind"
      >
        <v-carousel-item v-for="(item, i) in questions" :key="i">
          <v-row
            justify="start"
            class="ques-text px-3
            pt-6 text-h5
            text-md-h4"
            id="ques_no"
            >
            Question {{ i + 1 }}
            </v-row
          >
          <v-row
            justify="start"
            id="ques-detail"
            class="ques-text pb-4 pl-3 
            text-h6
            text-md-h5
            text-lg-h4"
            v-html="item.ques"
            >{{ item.ques }}</v-row
          >

          <v-row class="pr_row" v-if="item.img != null">
            <div class="parent_img mt-2">
              <img class="pr_img" :src="item.img" />
            </div>
          </v-row>

          <v-row justify="start">
            <v-textarea
              label="Write your answer"
              outlined
              class="mt-2 ami joss shottti boltesi px-3
              text-subtitle-1
              text-md-h6"
              rows="3"
              v-model="answers[i]"
            ></v-textarea>
          </v-row>

          <v-row justify="end" class="px-2">
            <v-btn
              class="submit text-subtitle-1 font-weight-black mb-10 mr-2"
              color="transparent"
              elevation="6"
              @click="fun(i)"
              :loading="loader"
              :disabled="loader"
            >
              Submit
              <!-- <v-icon class="mr-2 pl-2"> mdi-telegram </v-icon> -->
              <template v-slot:loader>
                <span class="custom-loader">
                  <v-icon light>mdi-cached</v-icon>
                </span>
              </template>
            </v-btn>

            <!-- <v-btn class="submit text-h6 font-weight-black"  color="transparent"> Next <v-icon class="ml-2"> mdi-arrow-right </v-icon> </v-btn> -->
          </v-row>
        </v-carousel-item>
      </v-carousel>
    </div>

    <v-btn
      fab
      class="nav-btn mdibtn"
      color="transparent"
      elevation="24"
      @click="ques_bar = !ques_bar"
    >
      <v-icon class="mdicon"> mdi-arrow-right </v-icon>
    </v-btn>

    <v-navigation-drawer v-model="ques_bar" fixed temporary class="nav-drawer">
      
      <div class="logout">
        <!-- eta responsive korte hbe -->
        <div class="info-text text-h5 mt-8"> {{ user_name }} <v-icon size="40px" class="ic"> mdi-ninja </v-icon> </div>
        <v-btn class="lgout my-8" elevation="" @click="logout()" rounded> Logout </v-btn>
      </div>
        <v-divider />

      <button
        v-for="index in questions.length"
        :key="index"
        :class="questions[index-1].attempted == 1 ? 'ques-btn-attempt' : 'ques-btn'"
        large
        @click="do_it(index - 1)"
      >
        <span v-if="questions[index - 1].attempted == 1">
          Question {{ index }}
        </span>
        <span v-else> Question {{ index }} </span>
      </button>
    </v-navigation-drawer>

    <v-snackbar class="pt-2 pr-1" absolute top right v-model="snackbar" :timeout="timeout">
      {{ snacktext }}

      <template v-slot:action="{ attrs }">
        <v-btn color="blue" text v-bind="attrs" @click="snackbar = false">
          Close
        </v-btn>
      </template>
    </v-snackbar>
  </div>
</template>


<script>
import Timer from "@/components/Timer3.vue";
var base_link = "https://pihacks-btc-api.herokuapp.com";

export default {
  components: { Timer },
  props: {
    user_name: String,
    questions:Array[Object],
    endTime: {
      type: Number,
      default: 0,
    },
    answers:{
      type: Array[String],
      default:null
    }
  },
  data() {
    return {
      img: 1,
      ques_bar: null,
      loader: false,
      ind: 0,
      snackbar: false,
      snacktext: "",
      timeout: 2000,
    };
  },
  watch:{
    questions(){
      if(this.answers == null) {
        this.answers = [];
      }
      for(let i=0;i<this.questions.length;i++){
        if(this.answers.length == i) {
          this.answers[i] = "";
        }
        if(this.answers[i] != "") {
          this.questions[i].attempted = true;
        }
      }
    }
  },
  methods: {
    logout(){
      let code = 0;
      fetch(base_link + "/btc", {
        method: "DELETE",
        credentials: "include",
        headers: {
          "Content-Type": "application/json",
        },
      })
      .then((data) => {
        code = data.status;
        return data.json();
      })
      .then((res) => {
        if(code != 200 || res.status != "success") {
          this.snackbar= true;
          this.text=res.message;
          return;
        }
        if(window.Storage != null)
        {
          window.localStorage.removeItem("uid");
          window.localStorage.setItem("loggedout", true);
        }
        window.location.reload();
      })
    },

    fun(ques_no){
      this.loader = true;
      let apibody = {
        answer: this.answers[ques_no].trim()
      };
      console.log(this.answers[ques_no].trim());
      this.loader = true;
      let code = 0;
      fetch(base_link + '/btc/' + ques_no, {
        method: "PATCH",
        credentials: "include",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(apibody)
      })
      .then((data) => {
        code = data.status;
        return data.json();
      })
      .then((res) => {
        this.loader = false;
        if (code != 200 || res.status != "success") {
          this.snacktext = res.status + ": " + res.message;
          this.snackbar = true;
          return;
        }
        console.log("Submitted Successfully", res);
        this.snackbar = true;
        this.answers[ques_no] = "";
        this.snacktext = "Answer submitted successfully";
        this.questions[this.ind].attempted = 1;
      })
    },

    next() {
      this.ind = (this.ind + 1) % this.questions.length;
    },
    back() {
      this.ind = (this.questions.length + this.ind - 1) % this.questions.length;
    },
    do_it(id) {
      this.ques_bar = !this.ques_bar;
      this.ind = id;
    },
  }
};
</script>

<style>

.v-application .text-h4{
  font-family: "fkpieceofshit" !important;
}

.ic{
  align-self: center;
}

.nav-drawer{
  background-color: rgb(32, 32, 32) !important;
}

.lgout{
  color: rgb(0, 0, 0) !important;
  background-color: rgb(175, 181, 190) !important;
  font-size: 18px !important;
  width: 110px;
  /* font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif; */
  font-weight: 900 !important;
  height: 40px !important;
}

.lgout:hover {
  color: rgb(146, 228, 255) !important;
  background-color: rgb(6, 27, 41) !important;
}

.logout{
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

.v-btn{
  text-transform: none !important; 
}

@font-face {
  font-family: fkpieceofshit;
  src: url("../assets/VCR_OSD_MONO.ttf");
}

.v-application .text-md-h5 .text-h6 .text-md-h3 .text-h4 .text-subtitle-1 {
  font-family: "fkpieceofshit" !important;
}

#speci {
  width: 100%;
  height: 100%;
  display: flex;
  align-content: center;
  justify-content: center;
  text-align: center;
  background-color: rgb(27, 77, 158);
}

.custom-loader {
  animation: loader 1s infinite;
  display: flex;
}
@-moz-keyframes loader {
  from {
    transform: rotate(0);
  }
  to {
    transform: rotate(360deg);
  }
}
@-webkit-keyframes loader {
  from {
    transform: rotate(0);
  }
  to {
    transform: rotate(360deg);
  }
}
@-o-keyframes loader {
  from {
    transform: rotate(0);
  }
  to {
    transform: rotate(360deg);
  }
}
@keyframes loader {
  from {
    transform: rotate(0);
  }
  to {
    transform: rotate(360deg);
  }
}

.pinit {
  display: flex;
}
.init {
  align-self: flex-end;
}
.last {
  display: flex;
  justify-content: flex-end !important;
}

.pr_row {
  margin: 0px !important;
  display: flex !important;
  justify-content: center !important;
}

.body {
  height: 100%;
  display: flex;
  justify-content: center;
}

.mein {
  max-width: 800px;
  width: 100%;
  margin-top: 30px;
}

.v-application p {
  margin-bottom: 0 !important;
}

b, strong{
  font-weight: 600 !important;
}

p {
  font-family: 'Courier New', Courier, monospace;
  font-weight: 400 !important;
}

/* .v-textarea textarea {
    padding: 5px !important;
} */

.v-textarea textarea .ami.joss.shottti.boltesi{
    padding: 5px !important;
}


@keyframes transitionLeft {
  from {
    opacity: 0;
    transform: translateX(-400px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

@keyframes transitionRight {
  from {
    opacity: 0;
    transform: translateX(400px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

.previous {
  background-color: #f1f1f1;
  color: black;
}

.next {
  background-color: #04aa6d;
  color: white;
}

.round {
  border-radius: 50%;
}

.v-textarea textarea {
  padding: 10px !important;
}

.line {
  width: 100% !important;
  opacity: 0.6;
  border-bottom: 2px solid lightblue;
}

.pr_img {
  height: 100%;
  width: 100%;
  object-fit: contain;
  filter: brightness(60%);
}

.ques-btn {
  font-size: 21px;
  width: 100%;
  font-weight: 600;
  text-align: center;
  border-bottom: 1px double grey;
  background-color: rgb(31, 31, 31);
  height: 45px;
}

.ques-btn:hover {
  background-color: rgb(9, 11, 14) !important;
}

.ques-btn-attempt {
  font-size: 21px;
  width: 100%;
  font-weight: 600;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  border-bottom: 1px double grey;
  background-color: rgb(27, 77, 158);
  height: 45px;
}

.ques-btn-attempt:hover {
  background-color: rgb(9, 11, 14) !important;
}

#ques-no{
  /* font-weight: 100 !important; */
}

.ques-text {
  font-size: 35px;
  width: 100% !important;
  /* font-weight: 200 !important; */
  color: #a5e5d4 !important;
  will-change: contents, width !important;
  /* font-family: "M PLUS 1p", "Open Sans", sans-serif !important; */
  /* font-family: "fkpieceofshit" !important; */
  text-shadow: 1px 2px 5px rgb(165 229 212 / 50%) !important;
  /* text-shadow: 0 0 20px rgb(37, 38, 39),  0 0 20px rgba(10, 175, 230, 0) !important; */
}

.txt {
  font-size: 30px !important;
  color: #a5e5d4 !important;
  font-weight: 400 !important;
  text-shadow: 0.5px 1.5px 3px rgb(165 229 212 / 50%) !important;
  -webkit-animation: an 0.9s infinite alternate !important;
  animation: an 0.9s infinite alternate !important;
  transition: border-color 0.1s, color 0.1s, text-shadow 0.1s,
    transform 0.3s 1.2s !important;
}

.nav-btn {
  background-color: transparent !important;
  position: absolute !important;
  left: 20px;
  top: 50%;
  transform: translateY(-50%);
}

.submit:hover {
  background-color: black !important;
  color: rgb(146, 228, 255) !important;
}

#ques_no {
  display: inline-block;
  font-family: "fkpieceofshit" !important;
}

#ques-detail {
  /* font-family: "M PLUS 1p", "Open Sans", sans-serif !important; */
  /* font-family: "fkpieceofshit" !important;
  text-transform: uppercase; */
  font-weight: 400 !important;
}
@media only screen and (max-width:970px) {
  .nav-btn {
    margin-top: 0px;
    top: 0;
    left: 0;
    transform: translateY(0%);
  }
}


@media only screen and (min-width: 1264px) {
  .mein {
    max-width: 1000px;
  }
}
@media only scree and (min-width: 960px) {
  
.txt {
  font-size: 40px !important;
}
}
@media only screen and (min-width: 1580px) {
  .mein {
    max-width: 1300px;
  }
}
</style>
