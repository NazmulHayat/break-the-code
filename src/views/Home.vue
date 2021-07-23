<template>
  <div class="main">
    <!-- <span v-if="show_time==1"> <Timer /> </span> -->
    <div id="welcome">
      <div id="glitched-writer"></div>
    </div>
    <div v-if="show_time == 0" id="inp">
      <div id="child-inp">
        <input class="input" placeholder="$ Your ID" autocomplete="off" />
        <input class="input" placeholder="$ Your Password" autocomplete="off" />
        <!-- <div class="input--shadow"></div> -->
        <button id="proceed" class="pl-2" type="button" @click="next()">
          <v-icon size="52px" id="ic" color="#a5e5d4" elevation="24">
            mdi-arrow-right
          </v-icon>
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import GlitchedWriter, { glyphs } from "glitched-writer";
// import Timer from '@/components/Timer2.vue'

export default {
  data() {
    return {
      show_time: 0,
    };
  },
  components: {
    // Timer
  },
  methods: {
    next() {
      // var ok = check()
      var ok = 1;
      this.show_time = 1;
      document.getElementById("glitched-writer").style.top = "25px";
      if (ok) {
        console.log("hurray");
      }
    },
  },
  mounted() {
    const writer = new GlitchedWriter("#glitched-writer", "encrypted");
    writer.options.extend({
      glyphs: glyphs.letterlike,
    });
    const phrases = ["Welcome to", "Break the Code"];
    writer.queueWrite(phrases, 1000, false);
  },
};
</script>




<style lang="scss" scoped>
.main {
  height: 100%;
}
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

#welcome {
  width: 100%;
  text-align: center;
}

#glitched-writer {
  // padding: 30px;
  font-size: 100px !important;
  color: $light-blue;
  will-change: contents, width;

  @include font-family;
  @include text-shadow($light-blue);

  &::after,
  &::before {
    content: attr(data-gw-string);
    position: absolute;
    opacity: 0;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    padding: 30px;
    overflow: hidden;
    white-space: nowrap;
    color: $blue;
    will-change: contents, width;
  }
  &::before {
    z-index: -1;
    color: $pink;
  }
  &.gw-writing {
    animation: glitch-skew 1s steps(10, end) infinite alternate-reverse;

    .gw-ghosts,
    .gw-glitched {
      opacity: 0.6;
      animation: glitch-blink 1s steps(20, end) infinite alternate-reverse;
    }

    &::after,
    &::before {
      opacity: 1;
    }
    &::after {
      animation: glitch-animation-1 1.5s steps(20, end) infinite
        alternate-reverse;
    }
    &::before {
      animation: glitch-animation-2 2s steps(20, end) infinite alternate-reverse;
    }
  }
  @keyframes glitch-skew {
    $steps: 10;

    @for $i from 0 through $steps {
      #{percentage($i * 1 / $steps)} {
        transform: skew(random(10) - 5 + deg);
      }
    }
  }
  @keyframes glitch-blink {
    $steps: 20;

    @for $i from 0 through $steps {
      #{percentage($i * 1 / $steps)} {
        opacity: random(10) / 10;
      }
    }
  }
  @keyframes glitch-animation-1 {
    $steps: 20;

    @for $i from 0 through $steps {
      #{percentage($i * 1 / $steps)} {
        clip: rect(random(100) + px, 1000px, random(100) + px, 0);
        transform: skew(random(16) - 8 + deg) translatex(random(30) - 15 + px);
      }
    }
  }
  @keyframes glitch-animation-2 {
    $steps: 20;

    @for $i from 0 through $steps {
      #{percentage($i * 1 / $steps)} {
        clip: rect(random(100) + px, 1000px, random(100) + px, 0);
        transform: skew(random(10) - 5 + deg) translatex(random(20) - 10 + px);
      }
    }
  }
}

#inp {
  height: 100%;
  width: 100%;
  position: absolute;
  top: 0;
  left: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  justify-items: center;
}

#child-inp * {
  display: block;
}

#ic:hover {
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

@media only screen and(max-width: 1350px) {
  #glitched-writer {
    font-size: 80px !important;
  }
}

@media only screen and(max-width: 1100px) {
  #glitched-writer {
    font-size: 70px !important;
  }
}

@media only screen and(max-width: 950px) {
  #glitched-writer {
    font-size: 60px !important;
  }
}

@media only screen and(max-width: 950px) {
  #glitched-writer {
    font-size: 60px !important;
  }
}

@media only screen and(max-width: 820px) {
  #glitched-writer {
    font-size: 45px !important;
  }
}
</style>