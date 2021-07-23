<template>
  <div class="container">
    <h1>Before Start</h1>
    <div id="countdown">
      <ul class="mx-16">
        <li><span id="days"></span>days</li>
        <li><span id="hours"></span>Hours</li>
        <li><span id="minutes"></span>Minutes</li>
        <li><span id="seconds"></span>Seconds</li>
      </ul>
    </div>
  </div>
</template>


<script>
export default {
  mounted() {
    const second = 1000,
      minute = second * 60,
      hour = minute * 60;
    let countDown = Date.now() + 1000 * 10 * 1,
      x = setInterval(function () {
        let distance = countDown - Date.now();
        if (distance <= 0) {
          clearInterval(x);
          document.getElementById("days").innerText = 0;
          document.getElementById("hours").innerText = 0;
          document.getElementById("minutes").innerText = 0;
          document.getElementById("seconds").innerText = 0;
          return;
        }
        document.getElementById("days").innerText = Math.floor(distance / day);
        document.getElementById("hours").innerText = 
          Math.floor((distance % day) / hour);
        document.getElementById("minutes").innerText =
          Math.floor((distance % hour) / minute);
        document.getElementById("seconds").innerText =
          Math.floor((distance % minute) / second);
        //seconds
      }, 0);
  },
};
</script>

<style scoped>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

html,
body {
  height: 100%;
  margin: 0;
}

body {
  align-items: center;
  background-color: #ffd54f;
  display: flex;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
    Oxygen-Sans, Ubuntu, Cantarell, "Helvetica Neue", sans-serif;
}

ul {
  padding: 0;
}

.container {
  position: absolute;
  top: 50%;
  left: 50%;
  -webkit-transform: translateX(-50%) translateY(-50%);
  transform: translateX(-50%) translateY(-50%);
  color: rgb(255, 255, 255);
  margin: 0 auto;
  text-align: center;
  text-shadow: 0 0 20px rgba(10, 175, 230, 1), 0 0 20px rgba(255, 255, 255, 0) !important;
}

h1 {
  font-weight: normal;
  letter-spacing: 0.125rem;
  text-transform: uppercase;
}

li {
  display: inline-block;
  font-size: 1.5em;
  list-style-type: none;
  padding: 1em;
  text-transform: uppercase;
}

li span {
  display: block;
  font-size: 4.5rem;
}

@media all and (max-width: 768px) {
  h1 {
    font-size: 1.5rem;
  }

  li {
    font-size: 0.5rem;
    padding: 0.75rem;
  }

  li span {
    font-size: 3.375rem;
  }
}
</style>
