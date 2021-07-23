
<script>
// const GlitchedWriter = require("https://cdn.skypack.dev/vue-glitched-writer@1.0.8");
import GlitchedWriter from "https://cdn.skypack.dev/vue-glitched-writer";

// Glitched Writer vue component:
// https://www.npmjs.com/package/vue-glitched-writer

console.log("asdasD", GlitchedWriter);

export default {
  components: {
    GlitchedWriter,
  },
  data() {
    return {
      messages: [
        "Deep in the human unconscious",
        "is a pervasive need,",
        "for a logical universe",
        "that makes sense.",
        "But the real universe",
        "is always one step beyond logic.",
        "― Frank Herbert, Dune",
      ],
      options: { letterize: true },
      queueOptions: { loop: 800 },
    };
  },
};
</script>

<template>
  <div id="app">
    <div class="planet"></div>
    <GlitchedWriter
      :text="messages"
      appear
      preset="cosmic"
      :options="options"
      :queue="queueOptions"
      tag="h1"
    />

    <a
      class="npm"
      href="https://www.npmjs.com/package/vue-glitched-writer"
      target="_blank"
    >
      <svg viewBox="0 0 780 250">
        <path
          d="M240,250h100v-50h100V0H240V250z M340,50h50v100h-50V50z M480,0v200h100V50h50v150h50V50h50v150h50V0H480z M0,200h100V50h50v150h50V0H0V200z"
        ></path>
      </svg>
    </a>
    <div class="noise"></div>
  </div>
</template>

<style lang="scss">
$black: #03071e;
$white: #e7eafd;
$red: #9d0208;
html {
  color: $white;
  font-family: "Inconsolata", monospace;
}
::selection {
  background: $red;
}
body {
  background: $black;
  width: 100vw;
  height: 100vh;
  overflow: hidden;
}
h1 {
  position: fixed;
  top: 25%;
  left: 20%;
  will-change: contents;
  white-space: pre-wrap;
  display: flex;
  text-transform: uppercase;
  text-shadow: 0px 0px 2px rgba($white, 0.6);
  filter: blur(0.2px);

  .gw-char {
    display: flex;
    justify-content: center;
    width: 1.5rem;
    animation: glitch-blink 1s steps(20, end) infinite alternate-reverse;
    animation-delay: 300ms;
    &:nth-child(4n) {
      animation-delay: 500ms;
    }
    &:nth-child(4n + 1) {
      animation-delay: 700ms;
    }
    &:nth-child(4n + 2) {
      animation: none;
    }
  }
}

.planet {
  position: absolute;
  right: -15vw;
  bottom: -30vh;
  width: 110vmin;
  height: 110vmin;
  border-radius: 50%;
  background: $red;
  background: -webkit-radial-gradient(bottom left, $red, $black);
  filter: blur(0.6px);
}

@keyframes glitch-blink {
  $steps: 20;

  @for $i from 0 through $steps {
    #{percentage($i * 1 / $steps)} {
      opacity: 0.65 + random(10) / 10;
    }
  }
}

.npm {
  position: absolute;
  right: 30px;
  bottom: 30px;
  svg {
    width: 80px;
    fill: $black;
  }

  &:hover {
    svg {
      fill: $white;
    }
  }
}

@keyframes grain {
  0%,
  100% {
    transform: translate(0, 0);
  }
  10% {
    transform: translate(-10px, -20px);
  }
  20% {
    transform: translate(-20px, 10px);
  }
  30% {
    transform: translate(10px, -25px);
  }
  40% {
    transform: translate(-10px, 50px);
  }
  50% {
    transform: translate(40px, 30px);
  }
  60% {
    transform: translate(40px, 0);
  }
  70% {
    transform: translate(0, 15px);
  }
  80% {
    transform: translate(5px, 100px);
  }
  90% {
    transform: translate(-30px, 20px);
  }
}

.noise {
  position: absolute;
  top: -100px;
  left: -100px;
  bottom: -100px;
  right: -100px;
  opacity: 0.5;
  pointer-events: none;
  animation: grain 8s steps(5) infinite alternate;
  background-image: url(data:image/png;base64,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);
}
</style>
