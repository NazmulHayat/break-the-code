<template>
  <div id="mein_wr">
    <v-btn class="lgout2 my-8 mr-8" elevation="" @click="logout()" rounded large> Logout </v-btn>
    <div class="container">
      <h1>Before Start</h1>
      <div id="countdown">
        <ul class="">
          <li><span id="days"></span>days</li>
          <li><span id="hours"></span>Hours</li>
          <li><span id="minutes"></span>Minutes</li>
          <li><span id="seconds"></span>Seconds</li>
        </ul>
      </div>
    </div>
    <v-snackbar class="pt-2 pl-1" absolute top left v-model="snackbar" :timeout="timeout">
      {{ snacktext }}

      <template v-slot:action="{ attrs }">
        <v-btn color="blue" text v-bind="attrs" @click="snackbar = false">
          Close
        </v-btn>
      </template>
    </v-snackbar>
  </div>
</template>


<script>

var base_link = "https://pihacks-btc-api.herokuapp.com";
export default {
  data() {
    return {
      snackbar: false,
      snacktext: "",
      timeout:2000,
    };
  },
  props: {
    start: {
      type: Number,
      default: Date.now() + 9000000,
    },
  },
  methods: {
    logout(){
      let code = 0;
      fetch(base_link + "/btc", {
        method: "DELETE",
        credentials: "include",
        headers: {
          "Content-Type": "application/json",
        },
      })
      .then((data) => {
        code = data.status;
        return data.json();
      })
      .then((res) => {
        if(code != 200 || res.status != "success") {
          this.snackbar= true;
          this.snacktext=res.message;
          return;
        }
        if(window.Storage != null)
        {
          // this.snackbar= true;
          // this.snacktext="yo yo hunny bunny";
          window.localStorage.removeItem("uid");
          window.localStorage.setItem("loggedout", true);
        }
        window.location.reload();
      })
    },
  },
  mounted() {
    console.log(this.start);
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
        document.getElementById("days").innerText = 0;
        document.getElementById("hours").innerText = 0;
        document.getElementById("minutes").innerText = 0;
        document.getElementById("seconds").innerText = 0;
        return;
      }
      document.getElementById("days").innerText = Math.floor(distance / day);
      document.getElementById("hours").innerText = Math.floor((distance % day) / hour);
      document.getElementById("minutes").innerText = Math.floor((distance % hour) / minute);
      document.getElementById("seconds").innerText = Math.floor((distance % minute) / second);
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

.lgout2{
  position: absolute !important;
  right: 0; top: 0;
  margin-right: 20px;
  color: rgb(0, 0, 0) !important;
  background-color: rgb(175, 181, 190) !important;
  font-size: 18px !important;
  width: 110px;
  /* font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif; */
  font-weight: 900 !important;
}

.lgout2:hover {
  color: rgb(146, 228, 255) !important;
  background-color: rgb(6, 27, 41) !important;
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

ul{
  display: flex;
  /* flex-direction: column; */
  justify-content: center;
  flex-wrap: wrap;
  /* align-items: center; */
}

@media all and (max-width: 768px) {

  li {
    font-size: 1.125rem;
    padding: .75rem;
  }
  
  li span {
    font-size: 4.5rem;
  }
}

@media all and (max-width: 410px) {

  li {
    font-size: 1rem;
    padding-right: 1.5rem;
    padding-bottom: 1.5rem;
  }
  
  li span {
    font-size: 3.5rem;
  }
}
</style>
