<template>
  <v-app id="app">
    <div class="animated" />
    <router-view />
    <Footer class="foot" />
  </v-app>
</template>

<script>
import Footer from "./components/Footer.vue";
export default {
  name: "App",
  components: { Footer },
  data: () => ({
    //
  }),
};
</script>

<style>
@font-face {
  font-family: fkpieceofshit;
  src: url("./assets/VCR_OSD_MONO.ttf");
}

html {
  overflow-y: auto !important;
}

.animated {
  width: 100vw;
  opacity: 0.8;
  z-index: -1;
  border-bottom: 2px solid rgb(147, 155, 155);
  filter: brightness(60%);
}

.animated {
  animation: MoveUpDown 20s linear infinite;
  position: absolute;
  left: 0;
  top: 0;
}

@keyframes MoveUpDown {
  0%,
  100% {
    top: 0vh;
  }
  50% {
    top: 92.5vh;
  }
}
/* #app {
  background-color: #050705;
  background-image: radial-gradient(rgba(66, 195, 200, 0.2), #000000 120%);
  background: #0f3854;
    background: radial-gradient(ellipse at center,  #050505  0%, #000000 95%);
  filter: brightness(170%);
}

#app::after {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: repeating-linear-gradient(
    0deg, 
    rgba(29, 30, 34, 0.5),
    rgba(22, 22, 22, 0.5) 0px,
    transparent 2px,
    transparent 5px
  );
  0D0F0D
  z-index: 0;
  pointer-events: none;
} */

@keyframes colorchange {
  from {
    /* opacity: 0.8; */
    /* background-image: radial-gradient(rgba(66, 195, 200, 0.2), #000000 120%); */
    /* background-image: radial-gradient(rgba(61, 56, 56, 0.2), #000000 120%); */
    background-color: black;
  }
  to {
    opacity: 1;
    background-image: radial-gradient(rgba(93, 84, 84, 0.2), #000000 120%);
  }
}


#app {
  background-color: #1d1e22;
  animation: colorchange 2.5s;
  background-image: radial-gradient(rgba(93, 84, 84, 0.2), #000000 120%);
  /* background: #0f3854;
    background: radial-gradient(ellipse at center,  #050505  0%, #000000 95%); */
  filter: brightness(170%);
}

#app::after {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: repeating-linear-gradient(
    0deg,
    rgba(29, 30, 34, 0.5),
    rgba(22, 22, 22, 0.5) 0px,
    transparent 2px,
    transparent 5px
  );
  pointer-events: none;
}

@media only screen and (max-width: 550px) {
  html,
  #app {
    /* overflow-y:hidden !important; */
    overflow-y: visible !important;
  }
}
</style>
