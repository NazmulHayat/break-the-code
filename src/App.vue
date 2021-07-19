<template>
  <v-app id="app">
    <div class="animated" />
    <v-main>
      <router-view/>
    </v-main>
    <Footer />
  </v-app>
</template>

<script>
import Footer from './components/Footer.vue'
export default {
  name: 'App',
  components: {Footer},
  data: () => ({
    //
  }),
};
</script>

<style>


.animated{
  width: 100vw;
  border-bottom: 2px solid rgb(68, 105, 116);
  filter: brightness(60%);
}

.animated {
  animation: MoveUpDown 20s linear infinite;
  position: absolute;
  left: 0;
  top: 0;
}

@keyframes MoveUpDown {
  0%, 100% {
    top: 0;
  }
  50% {
    top: 90vh;
  }
}

html, #app { 
  /* overflow-y:hidden !important; */
  overflow-x:hidden !important;
}
#app{
  background-color: #1d1e22;
  background-image: radial-gradient(rgba(66, 195, 200, 0.2), #000000 120%);
  filter: brightness(170%);
}

#app::after{
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: repeating-linear-gradient(
  0deg
  , rgba(29, 30, 34, 0.5), rgba(22, 22, 22, 0.5) 0px, transparent 2px, transparent 5px);
      pointer-events: none;
}

</style>
