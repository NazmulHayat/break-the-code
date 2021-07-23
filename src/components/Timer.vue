<template>
  <div class="ble pb-16 pt-5">
    <div id="flipdown" class="flipdown"></div>
  </div>
</template>

<script>
const flipdown = require("../assets/flipdown");
function WaitUntilFlipDownExists() {
  return new Promise((resolve, reject) => {
    setInterval(() => {
      if (document.getElementById("flipdown") != null) resolve();
    }, 10);
    let a = 0;
    if (a) reject(); //vue is shit
  });
}
export default {
  data: () => {
    return {};
  },
  methods: {
    dhet: async () => {
      await WaitUntilFlipDownExists();
      var twoDaysFromNow = new Date().getTime() / 1000 + 86400 * 2 + 1;
      var fku = new flipdown(
        twoDaysFromNow,
        document.getElementById("flipdown")
      );
      fku.start();
    },
  },
  beforeMount() {
    this.dhet();
  },
};
</script>

<style>
@import "../assets/flipdown.css";
.flipdown {
  padding-top: 20px;
  font-size: 1.5em;
  font-family: Cambria, Cochin, Georgia, Times, "Times New Roman", serif;
  margin: auto;
}
.ble {
  width: 100%;
}
</style>