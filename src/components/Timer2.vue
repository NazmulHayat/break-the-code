<template>
  <div id="mein_wr">
    <v-btn class="lgout2 my-8 mr-8" elevation="" @click="logout()" rounded large> Logout </v-btn>
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
    };
  },
  props: {
    start: {
      type: Number,
      default: 0,
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
  display: inline-block;
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
