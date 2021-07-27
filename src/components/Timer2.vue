<template>
  <div class="container">
    <h1>Before Start</h1>
    <div id="countdown">
      <ul class="mx-16">
        <li id="Hdays"></li>
        <li id="Hhours"></li>
        <li id="Hminutes"></li>
        <li id="Hseconds"></li>
      </ul>
    </div>
  </div>
</template>


<script>
export default {
  data() {
    return {};
  },
  props: {
    start: {
      type: Number,
      default: 0,
    },
  },
  mounted() {
    const second = 1000,
      minute = second * 60,
      hour = minute * 60,
      day = hour * 24;
    let x = setInterval(()=> {
      if (this.start == 0) {
        return;
      }
      let distance = this.start - Date.now();
      if (distance <= 0) {
        clearInterval(x);
        document.getElementById("Hdays").innerText = 0;
        document.getElementById("Hhours").innerText = 0;
        document.getElementById("Hminutes").innerText = 0;
        document.getElementById("Hseconds").innerText = 0;
        return;
      }
      document.getElementById("Hdays").innerText = Math.floor(distance / day) + " Days";
      document.getElementById("Hhours").innerText =
        Math.floor((distance % day) / hour) + " Hours";
      document.getElementById("Hminutes").innerText =
        Math.floor((distance % hour) / minute) + " Minutes";
      document.getElementById("Hseconds").innerText =
        Math.floor((distance % minute) / second) + " Seconds";
      //seconds
    }, 1);
  }
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
