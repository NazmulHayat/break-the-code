<template>
  <div class="main">
    <Timer />
    <glitched-writer text="Your Content" appear />
    <div id="inp">
      <input class="input" id="input" placeholder="$" autocomplete="off">
      <!-- <div class="input--shadow"></div> -->
      <button id="proceed" class="pl-2" type="button" @click="next()">
        <v-icon size="52px" id="ic" color="#a5e5d4" elevation="24"> mdi-arrow-right </v-icon>
      </button>
    </div>

  </div>
</template>

<script>

// import GlitchedWriter from 'vue-glitched-writer'
// import vueGlitchedWriter from 'https://cdn.skypack.dev/pin/vue-glitched-writer@v1.0.8-raV3eIK97fAHilXwleu8/mode=imports,min/optimized/vue-glitched-writer.js';
// const GlitchedWriter = require('vue-glitched-writer');
// console.log(vueGlitchedWriter);

import Timer from '@/components/Timer.vue';

export default{
  components: {
		// vueGlitchedWriter,
    Timer
	},
  methods:{
    next() {
      // var ok = check()
      var ok = 1;
      if(ok) {
        console.log("hurray");
      }
    }
  }
}

</script>




<style lang="scss" scoped>

* {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
*,
*::before,
*::after {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

$light-blue: #a5e5d4;
$blue: #42c3c8;
$pink: #d93da5;
$black: #1d1e22;
@mixin text-shadow($color) {
  text-shadow: 2px 4px 10px rgba($color, 0.5);
}
@mixin text-shadow-small($color) {
  text-shadow: 1px 3px 6px rgba($color, 0.5);
}
@mixin font-family {
  font-family: "M PLUS 1p", "Open Sans", sans-serif;
}

#inp{
  width: 100vw;
  margin: auto;
  display: flex;
  justify-content: center;
  position: absolute;
  top: 50%;
}

#ic:hover{
  filter: drop-shadow(3px 5px 2px rgb(0 0 0 / 0.4));
}

.input {
  // position: absolute;
  bottom: 30px;
  width: 340px;
  height: auto;
  padding: 0 8px;
  background: transparent;
  outline: none;
  border: 1px solid $light-blue;
  caret-color: $blue;
  color: $light-blue;
  font-weight: 300;
  font-size: 30px;
  @include text-shadow-small($light-blue);
  @include font-family;

  @keyframes an {
    0%,
    50% {
      ph: visible;
    }
    51%,
    100% {
      ph: hidden;
    }
  }

  animation: an 0.9s infinite alternate;
  transition: border-color 0.1s, color 0.1s, text-shadow 0.1s,
    transform 0.3s 1.2s;

  &::placeholder {
    color: $light-blue;
    transition: opacity 0.1s, color 0.1s;
    visibility: var(ph);

    @include text-shadow-small($light-blue);
  }
  &:focus,
  &:hover {
    border-color: $blue;
    color: $blue;

    @include text-shadow-small($blue);

    &::placeholder {
      color: $blue;
    }
    &::selection {
      background: $blue;
    }
    & ~ .input--shadow {
      border-color: $blue;
    }
  }
  &:focus::placeholder {
    opacity: 0;
  }
  &:disabled {
    transform: translatey(70px);

    & ~ .input--shadow {
      transform: translatey(70px);
    }
  }
  &--shadow {
    position: absolute;
    // top: 100%;
    // left: 30.5%;
    bottom: calc(30px - 4px);
    transform: translatex(2px);
    filter: blur(4px);
    opacity: 0.5;
    width: 340px;
    height: auto;
    border: 2px solid $light-blue;
    pointer-events: none;
    transition: transform 0.3s 1.2s;
  }
}
</style>