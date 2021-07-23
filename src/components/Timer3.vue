<template>
    <div class="timer-text">
      <span id="minutes" class="pr-2"></span>
      <span id="seconds"></span>
    </div>
</template>


<script>
const second = 1000,
  minute = second * 60,
  hour = minute * 60;
let birthday = "Sep 30, 2021 00:00:00",
  countDown = new Date(birthday).getTime(),
  x = setInterval(function () {
    let now = new Date().getTime(),
      distance = countDown - now;
    (document.getElementById("minutes").innerText =
      Math.floor((distance % hour) / minute) + "min"),
      (document.getElementById("seconds").innerText =
        Math.floor((distance % minute) / second) + "sec");
    //do something later when date is reached
    if (distance < 0) {
      clearInterval(x);
    }
    //seconds
  }, 0);
console.log(countDown);
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
  text-transform: lowercase;
}

li span {
  display: block;
  font-size: 2rem;
}
.timer-text{
  color: rgb(255, 255, 255);
  text-shadow: 0 0 20px rgba(10, 175, 230, 1), 0 0 20px rgba(255, 255, 255, 0);
  padding: 0px;
  display:inline-block;
  font-size:30px;
  text-transform: lowercase;
}
</style>
