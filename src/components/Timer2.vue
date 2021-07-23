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
(function () {
  const second = 1000,
    minute = second * 60,
    hour = minute * 60,
    day = hour * 24;

  let birthday = "Sep 30, 2021 00:00:00",
    countDown = new Date(birthday).getTime(),
    x = setInterval(function () {
      let now = new Date().getTime(),
        distance = countDown - now;

      (document.getElementById("days").innerText = Math.floor(distance / day)),
        (document.getElementById("hours").innerText = Math.floor(
          (distance % day) / hour
        )),
        (document.getElementById("minutes").innerText = Math.floor(
          (distance % hour) / minute
        )),
        (document.getElementById("seconds").innerText = Math.floor(
          (distance % minute) / second
        ));

      //do something later when date is reached
      if (distance < 0) {
        let headline = document.getElementById("headline"),
          countdown = document.getElementById("countdown"),
          content = document.getElementById("content");

        headline.innerText = "It's my birthday!";
        countdown.style.display = "none";
        content.style.display = "block";

        clearInterval(x);
      }
      //seconds
    }, 0);
})();
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
