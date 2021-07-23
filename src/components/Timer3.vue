<template>
    <div class="container">
        <div id="countdown">
            <ul class="">
            <li><span id="minutes" class="pr-2"></span></li>
            <li><span id="seconds"></span></li>
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
        console.log(day);
  let birthday = "Sep 30, 2021 00:00:00",
      countDown = new Date(birthday).getTime(),
      x = setInterval(function() {    

        let now = new Date().getTime(),
            distance = countDown - now;

        //   document.getElementById("hours").innerText = Math.floor((distance % (day)) / (hour)),
          document.getElementById("minutes").innerText = Math.floor((distance % (hour)) / (minute)) + 'min',
          document.getElementById("seconds").innerText = Math.floor((distance % (minute)) / second) + 'sec';

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
      }, 0)
  }());

</script>

<style scoped>

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

html, body {
  height: 100%;
  margin: 0;
}

body {
  font-family: -apple-system, 
    BlinkMacSystemFont, 
    "Segoe UI", 
    Roboto, 
    Oxygen-Sans, 
    Ubuntu, 
    Cantarell, 
    "Helvetica Neue", 
    sans-serif;
}

ul{
    padding: 0;
}

.v-application ul{
  padding: 0px !important;
}
.container {
  color: rgb(255, 255, 255);
  margin: 0 auto;
  /* padding: none !important; */
  text-align: center;
  text-shadow: 0 0 20px rgba(10, 175, 230, 1),  0 0 20px rgba(255, 255, 255, 0) !important;
}

h1 {
  font-weight: normal;
  letter-spacing: .125rem;
  text-transform: lowercase;
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
  font-size: 2.0rem;
}

@media all and (max-width: 768px) {
  h1 {
    font-size: 1.5rem;
  }
  
  li {
    font-size: 0.5rem;
    /* padding: .75rem */
  }
  
  li span {
    font-size: 1.375rem;
  }
}

.container{
    width: 100%;
    padding: 0px !important;
    margin-right: auto;
    margin-left: auto;
}

</style>
