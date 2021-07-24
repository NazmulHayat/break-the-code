<template>
  <div class="timer-text">
    <span id="minutes" class="pr-2"></span>
    <span id="seconds"></span>
  </div>
</template>


<script>
export default {
  mounted() {
    const second = 1000,
      minute = second * 60,
      hour = minute * 60;
    let countDown = Date.now() + 1000 * 60 * 60 ,
      x = setInterval(function () {
        let distance = countDown - Date.now();
        if (distance <= 0) {
          clearInterval(x);
          document.getElementById("minutes").innerText = "Contest";
          document.getElementById("seconds").innerText = "ended";
          return;
        }
        document.getElementById("minutes").innerText =
          Math.floor((distance % hour) / minute) + "min";
        document.getElementById("seconds").innerText =
          Math.floor((distance % minute) / second) + "sec";
        //seconds
      }, 0);
  },
};
</script>

<style scoped>
body {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
    Oxygen-Sans, Ubuntu, Cantarell, "Helvetica Neue", sans-serif;
}

ul {
  padding: 0;
}

li {
  display: inline-block;
  font-size: 1.5em;
  list-style-type: none;
  /* padding: 1em; */
}

li span {
  display: block;
  font-size: 2rem;
}
.timer-text {
  color: rgb(255, 255, 255);
  text-shadow: 0 0 20px rgba(10, 175, 230, 1), 0 0 20px rgba(255, 255, 255, 0);
  padding: 0px;
  display: inline-block;
  font-size: 30px;
  text-transform: lowercase;
}
</style>
