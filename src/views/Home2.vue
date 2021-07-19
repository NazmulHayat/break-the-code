<template>
    <v-container fill-height class="mein d-flex pa-16 align-content-center">
      <!-- <v-container class="card ma-8 pr-1">
        <span  class="d-flex align-end flex-column">

        </span>
      </v-container> -->
      <v-row justify="start" id="ques-text" class="ques_no pb-2 text-md-h5 text-h6"> Question {{ind}}: </v-row>
      <v-row justify="start" id="ques-text" class="pb-4 text-md-h3 text-h4"> What the duck is your name? </v-row>
      <v-row> <v-img v-if="img==true"  class="pr_img mb-8" src="https://picsum.photos/1000/400"> </v-img> </v-row>
      <v-row justify="start">
        <v-textarea
          label="Write your answer"
          outlined
          class="txt"
          rows="4"
        ></v-textarea>
      </v-row>
      <v-row justify="end">
        <v-btn class="bcknext text-h6 font-weight-black mr-2"  color="transparent"> <v-icon class="mr-2"> mdi-arrow-left </v-icon> Back  </v-btn>
        <v-btn class="bcknext text-h6 font-weight-black"  color="transparent"> Next <v-icon class="ml-2"> mdi-arrow-right </v-icon> </v-btn>
      </v-row>
      <v-btn
        fab large
        class="nav-btn" 
        color="transparent" elevation="24"
        @click="ques_bar=!ques_bar"
      >
        <v-icon class="mdicon" size="45px"> mdi-arrow-left </v-icon>
      </v-btn>
      <v-navigation-drawer
        v-model="ques_bar"
        absolute
        temporary
        right
      >
        <button v-for="index in ques_len" :key="index" class="ques-btn" large>
            Question {{index}}
        </button>
      </v-navigation-drawer>
    </v-container>
</template>


<script>
  export default{
    data () {
      return {
        ques_len : 20,
        img: 1,
        ques_bar: null,
        ind: 1
      }
    },
  }
</script>

<style>

.v-textarea textarea{
  padding: 10px !important;
}
/* 
.card::-webkit-scrollbar {
  width: 11px;
}
.card {
  scrollbar-width: thin;
  scrollbar-color: var(--thumbBG) var(--scrollbarBG);
}
.card::-webkit-scrollbar-track {
  background: var(--scrollbarBG);
}
.card::-webkit-scrollbar-thumb {
  background-color: var(--thumbBG);
  border-radius: 6px;
  border: 3px solid var(--scrollbarBG);
} */

.mein{
  max-width: 1000px !important;
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
    color: #a5e5d4 !important;
    will-change: contents, width !important;
    font-family: "M PLUS 1p", "Open Sans", sans-serif !important;
    text-shadow: 2px 4px 10px rgb(165 229 212 / 50%) !important
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
  right: 20px;
  /* top: 50%; */
}

.bcknext:hover{
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
    margin-top: 30px;
    top: 0;
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
