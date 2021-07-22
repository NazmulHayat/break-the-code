<template>
    <v-container fill-height id="mein" class="mein mt-5 d-flex  align-content-center">
      <!-- <v-container class="card ma-8 pr-1">
        <span  class="d-flex align-end flex-column">

        </span>
      </v-container> -->
      <v-row justify="space-between" class="px-3" id="header"> 
        <div class="timer pt-2">
          <Timer />
        </div>
        <div class="btns d-flex pb-1">
          <v-btn v-if="ind!=1" fab color="transparent" id="back" elevation="1"><v-icon size="32px" @click="back()"> mdi-arrow-left </v-icon></v-btn>
          <v-btn v-if="ind!=4" fab color="transparent" id="next" elevation="1"><v-icon size="32px" @click="next()"> mdi-arrow-right </v-icon></v-btn>
        </div>
      </v-row>
      <div class="line pt-3"></div>
      <v-row justify="start" id="ques-text" class="ques_no pb-1 px-3 pt-9 text-md-h5 text-h6"> Question {{ind}}: </v-row>
      <v-row justify="start" id="ques-text" class="pb-4 text-md-h3 px-3 text-h4"> {{questions[ind]}} </v-row>
      <v-row> <v-img v-if="img==true"  class="pr_img mb-8 mx-4" src="https://picsum.photos/1000/400"> </v-img> </v-row>
      <v-row justify="start">
        <v-textarea
          label="Write your answer"
          outlined
          class="txt px-4"
          rows="4"
        ></v-textarea>
      </v-row>
      <v-row justify="end" class="px-2">
        <v-btn class="submit mb-10 text-subtitle-1 font-weight-black mr-2"  color="transparent" elevation="6">  Submit 
          <!-- <v-icon class="mr-2 pl-2"> mdi-telegram </v-icon> -->
          </v-btn>
        <!-- <v-btn class="submit text-h6 font-weight-black"  color="transparent"> Next <v-icon class="ml-2"> mdi-arrow-right </v-icon> </v-btn> -->
      </v-row>
      <v-btn
        fab large
        class="nav-btn" 
        color="transparent" elevation="24"
        @click="ques_bar=!ques_bar"
      >
        <v-icon class="mdicon" size="45px"> mdi-arrow-right </v-icon>
      </v-btn>
      <v-navigation-drawer
        v-model="ques_bar"
        absolute
        temporary
        left
      >
        <button v-for="index in ques_len" :key="index" class="ques-btn" large @click="do_it(index)">
            Question {{index}}
        </button>
      </v-navigation-drawer>
    </v-container>
</template>


<script>

  import Timer from '@/components/Timer3.vue';

  export default{
    components : {Timer},
    data () {
      return {
        ques_len : 5,
        img: 1,
        ques_bar: null,
        ind: 1,
        questions: [
          "dummy", "What the duck is your name?", "What is an apple?", "Why is life so unfair?",
          "What is your willpower?", "Hello hunny bunny"
        ]
      }
    },
    methods : {
      next () {
        this.ind++;
        document.getElementById('mein').style.animation = "transitionRight 1.0s";
      },
      back () {
        this.ind--; 
        document.getElementById('mein').style.animation = "transitionLeft 1.0s";
      },
      do_it(id){
        // var tmp = this.ind;
        this.ques_bar=!this.ques_bar;
        this.ind = id;
        // if(tmp < id) {
        //   document.getElementById('mein').style.animation = "transitionLeft 1.0s";
        // }
        // else if(tmp > id){
        //   document.getElementById('mein').style.animation = "transitionRight 1.0s";
        // }

      }
    }
  }
</script>

<style>
  @keyframes transitionLeft {
    from {
      opacity: 0;
      transform: translateX(-400px);
    }
    to{
      opacity: 1;
      transform: translateX(0);
    }
  }

  @keyframes transitionRight {
    from {
      opacity: 0;
      transform: translateX(400px);
    }
    to{
      opacity: 1;
      transform: translateX(0);
    }
  }

.submit{
}

.previous {
  background-color: #f1f1f1;
  color: black;
}

.next {
  background-color: #04AA6D;
  color: white;
}

.round {
  border-radius: 50%;
}


.v-textarea textarea{
  padding: 10px !important;
}

.line{
  width: 100% !important;
  opacity: 0.6;
  border-bottom: 2px solid lightblue;
}

.mein{
  max-width: 1000px !important;
  padding: 20px !important;
}

.card{
  position: absolute !important;
  top: 0;
  right: 0;
  max-width: 200px !important; 
  max-height: 30vh !important;
  overflow: auto;
}

.pr_img{
  height: auto;
  max-width: 1000px !important;
  width: 97%;
  filter: brightness(60%);
}

.ques-btn{
  font-size: 21px;
  width: 100%;
  padding: 15px;
  font-weight: 600;
  text-align: center;
  border-bottom: 1px double grey;
  /* box-shadow: 2px 2px rgb(66, 64, 64); */
  background-color:rgb(31, 31, 31);
}

.ques-btn:hover{
  background-color: rgb(48, 101, 172);
}

#ques-text{
    font-size: 35px;
    width: 100% !important;
    color: #a5e5d4 !important;
    will-change: contents, width !important;
    font-family: "M PLUS 1p", "Open Sans", sans-serif !important;
    text-shadow: 2px 4px 10px rgb(165 229 212 / 50%) !important
    /* text-shadow: 0 0 20px rgba(10, 175, 230, 1),  0 0 20px rgba(10, 175, 230, 0) !important; */
}

.txt{
  font-size: 30px !important;
  color: #a5e5d4 !important;
  font-weight: 400 !important;
  text-shadow: 1px 3px 6px rgb(165 229 212 / 50%) !important;
  font-family: "M PLUS 1p", "Open Sans", sans-serif !important;
  -webkit-animation: an 0.9s infinite alternate !important;
  animation: an 0.9s infinite alternate !important;
  transition: border-color 0.1s, color 0.1s, text-shadow 0.1s, transform 0.3s 1.2s !important;
}

.nav-btn{
  background-color: transparent !important;
  position: absolute !important;
  left: 20px;
  /* top: 50%; */
}

.submit:hover{
  background-color: black !important;
  color: rgb(146, 228, 255) !important;
}

.ques_no{
  display: inline-block;
}

/* #ques-txt::after, #ques-text::before{
    content: attr(data-gw-string) !important;
    position: absolute !important;
    opacity: 0 !important;
    left: 0;
    top: 0;
    width: 100% !important;
    height: 100% !important;
    padding: 30px !important;
    overflow: hidden !important;
    white-space: nowrap !important;
    color: #42c3c8 !important;
    will-change: contents, width !important;
} */

@media only screen and (max-width: 1195px) {
  .nav-btn{
    margin-top: 0px;
    top: 0;
    left: 0;
  }
}

@media only screen and (max-width: 700px) {
  .txt{
    font-size: 25px !important;
  }
}

@media only screen and (max-width: 550px) {
  .txt{
    font-size: 20px !important;
  }
  .mdicon{
    font-size: 35px !important;
  }
}

</style>
