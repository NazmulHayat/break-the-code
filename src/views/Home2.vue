<template>
  <div class="body">
    <div class="mein pa-3 pa-sm-5">
      <v-row dense>
        <v-col class="pinit">
          <Timer class="init 
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
            >Question {{ i + 1 }}</v-row
          >
          <v-row
            justify="start"
            id="ques-detail"
            class="ques-text pb-4 px-3 
            text-h4
            text-md-h3
            text-lg-h2"
            >{{ item.ques }}</v-row
          >

          <v-row class="pr_row" v-if="item.img != null">
            <div class="parent_img mb-2 mt-2">
              <img class="pr_img" :src="item.img" />
            </div>
          </v-row>

          <v-row justify="start">
            <v-textarea
              label="Write your answer"
              outlined
              class="txt px-3
              text-subtitle-1
              text-md-h6"
              rows="3"
            ></v-textarea>
          </v-row>

          <v-row justify="end" class="px-2">
            <v-btn
              class="submit text-subtitle-1 font-weight-black mb-10 mr-2"
              color="transparent"
              elevation="6"
              @click="fun()"
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

    <v-navigation-drawer v-model="ques_bar" absolute temporary left>
      <button
        v-for="index in questions.length"
        :key="index"
        class="ques-btn"
        large
        @click="do_it(index - 1)"
      >
        <span v-if="questions[index - 1].attempted == 1">
          <div id="speci">Question {{ index }}</div>
        </span>
        <span v-else> Question {{ index }} </span>
      </button>
    </v-navigation-drawer>

    <v-snackbar v-model="snackbar" :timeout="timeout" absolute bottom right>
      {{ text }}

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

export default {
  components: { Timer },
  data() {
    return {
      img: 1,
      ques_bar: null,
      loader: false,
      ind: 0,
      snackbar: false,
      text: "Your answer has been submitted.",
      timeout: 2000,
      questions: [
        {
          ques: "What is an apple?",
          img: "https://picsum.photos/1600/500",
          attempted: 0,
        },
        {
          ques: "What the duck is your name?",
          img: null,
          attempted: 1,
        },
        {
          ques: "Do you know Joe?",
          img: "https://picsum.photos/1600/400",
          attempted: 0,
        },
        {
          ques: "What is an ice-cream?",
          img: "https://picsum.photos/1600/400",
          attempted: 1,
        },
        {
          ques: "What is an orange?",
          img: null,
          attempted: 1,
        },
      ],
    };
  },
  methods: {
    fun() {
      this.loader = true;
      setTimeout(() => {
        this.loader = false;
        this.snackbar = true;
        this.questions[this.ind].attempted = 1;
      }, 2000);
    },
    next() {
      this.ind = (this.ind + 1) % this.questions.length;
    },
    back() {
      this.ind = (this.questions.length + this.ind - 1) % this.questions.length;
    },
    do_it(id) {
      console.log(id);
      this.ques_bar = !this.ques_bar;
      this.ind = id;
    },
  },
};
</script>

<style>
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
  background-color: rgb(98, 0, 211);
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
  display: flex !important;
  justify-content: center;
}

.mdibtn {
  height: 45px !important;
  width: 45px !important;
}
.mdicon {
  font-size: 35px !important;
}

.mein {
  max-width: 800px;
  width: 100%;
  margin-top: 30px;
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
  padding: 15px;
  font-weight: 600;
  text-align: center;
  border-bottom: 1px double grey;
  /* box-shadow: 2px 2px rgb(66, 64, 64); */
  background-color: rgb(31, 31, 31);
}

.ques-btn:hover {
  background-color: rgb(48, 101, 172);
}

.ques-text {
  font-size: 35px;
  width: 100% !important;
  color: #a5e5d4 !important;
  will-change: contents, width !important;
  /* font-family: "M PLUS 1p", "Open Sans", sans-serif !important; */
  /* font-family: "fkpieceofshit" !important; */
  text-shadow: 2px 4px 10px rgb(165 229 212 / 50%) !important;
  /* text-shadow: 0 0 20px rgba(10, 175, 230, 1),  0 0 20px rgba(10, 175, 230, 0) !important; */
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
  font-family: "fkpieceofshit" !important;
  text-transform: uppercase;
}
@media only screen and (max-width:970px) {
  .nav-btn {
    margin-top: 0px;
    top: 0;
    left: 0;
    transform: translateY(0%);
  }
}


@media only screen and (min-width: 750px) {
  .mdibtn {
    height: 50px !important;
    width: 50px !important;
  }
  .mdicon {
    font-size: 40px !important;
  }
}

@media only screen and (min-width: 1264px) {
  .mdibtn {
    height: 55px !important;
    width: 55px !important;
  }
  .mdicon {
    font-size: 45px !important;
  }
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
  .mdibtn {
    height: 60px !important;
    width: 60px !important;
  }
  .mdicon {
    font-size: 50px !important;
  }
  .mein {
    max-width: 1300px;
  }
}
</style>
