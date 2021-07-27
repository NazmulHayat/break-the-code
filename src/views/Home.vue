<template>
  <div class="mymain" id="mymain">
    <div class="home_login" v-if="!this.verified">
      <span v-if="show_time == 1"> <Timer /> </span>
      <div id="welcome">
        <div class="" id="glitched-writer"></div>
      </div>
      <div v-if="show_time == 0" id="inp">
        <div id="child-inp" class="mx-16">
          <!-- <input
            class="input"
            placeholder="$ Your ID"
            autocomplete="off"
            v-model="uid"
            v-on:keyup.enter="$event.target.nextElementSibling.focus()"
          />
          <input
            class="input mt-6"
            placeholder="$ Your Password"
            autocomplete="off"
            type="password"
            v-model="pass"
            v-on:keyup.enter="fun()"
          /> -->
          <!-- <div class="input--shadow"></div> -->
          <!-- <button id="proceed" class="pl-2" type="button" @click="next()">
            Next
          </button> -->

          <v-form ref="form" class="form">
            <v-text-field
              v-model="uid"
              label="$ Your ID:"
              class="text-field"
              color="black"
              :disabled="loader"
              outlined
              dark
              autocomplete="username"
              v-on:keyup.enter="focusNext()"
            ></v-text-field>
            <v-text-field
              v-model="pass"
              label="$ Your Password:"
              class="text-field"
              color="black"
              outlined
              dark
              :disabled="loader"
              id="password-field"
              autocomplete="new-password"
              type="password"
              v-on:keyup.enter="fun()"
            ></v-text-field>
          </v-form>
            <div
              class="amra pt-8 pb-2"
              style="display: flex; justify-content: center"
            >
              <v-btn
                class="submit mb-10 text-h6 font-weight-black mr-2"
                color="#a5e5d4"
                :loading="loader"
                :disabled="loader"
                large
                rounded
                outlined
                @click="fun()"
              >
                Login
                <!-- <v-icon class="mr-2 pl-2"> mdi-telegram </v-icon> -->
                <template v-slot:loader>
                  <v-icon class="custom-loader" light>mdi-cached</v-icon>
                </template>
              </v-btn>
            </div>
        </div>
      </div>
      <v-snackbar v-model="snackbar" :timeout="timeout">
        {{ snacktext }}
        <template v-slot:action="{ attrs }">
          <v-btn color="blue" text v-bind="attrs" @click="snackbar = false">
            Close
          </v-btn>
        </template>
      </v-snackbar>
    </div>
    <Ques v-if="verified == true" :user_name="uid" />
  </div>
</template>

<script>
import GlitchedWriter, { glyphs } from "glitched-writer";
import Timer from "@/components/Timer2.vue";
import Ques from "@/components/Ques.vue";
var base_link = "https://pihacks-btc-api.herokuapp.com";
export default {
  data() {
    return {
      loader: false,
      snackbar: false,
      timeout: 5000,
      show_time: 0,
      snacktext: "",
      uid: "",
      pass: "",
      verified: false,
    };
  },
  components: {
    Timer,
    Ques,
  },
  methods: {
      focusNext() {
        document.getElementById('password-field').focus();
      },
    fun() {
      let apibody = {
        uid: this.uid,
        pass: this.pass,
      };
      let code = 0;
      this.loader = true;
      fetch(base_link + "/btc", {
        method: "POST",
        credentials: "include",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(apibody),
      })
        .then((data) => {
          code = data.status;
          return data.json();
        })
        .then((res) => {
          this.loader = false;
          if (code != 200 || res.status != "success") {
            this.snacktext = res.status + ": " + res.message;
            this.snackbar = true;
            return;
          }
          this.verified = true;
          if(window.Storage != null){
            window.localStorage.setItem("uid",this.uid);
          }
        });
    },
  },
  mounted() {
    if(!this.verified){
      const writer = new GlitchedWriter("#glitched-writer", "encrypted");
      writer.options.extend({
        glyphs: glyphs.letterlike,
      });
      const phrases = ["Welcome to", "Break the Code"];
      writer.queueWrite(phrases, 1000, false);
    }
  },
  created() {
    if(window.Storage != null) {
      let uid = localStorage.getItem("uid");
      if(uid != null) { 
        this.uid=uid;
        this.verified = true;
      }
      else if(window.localStorage.getItem("timedout")) {
        this.snacktext= "Session timed out";
        this.snackbar= true;
        window.localStorage.removeItem("timedout");
      }
    }
    let code = 0;
    fetch(base_link + "/btc", {
      method: "GET",
      credentials: "include",
    })
      .then((data) => {
        code = data.status;
        return data.json();
      })
      .then((res) => {
        if (code != 200) {
          this.snacktext = res.status + ": " + res.message;
          this.snackbar = true;
          return;
        }
        if (res.verified == null && this.verified){
          window.localStorage.removeItem("uid");
          window.localStorage.setItem("timedout", true);
          window.location.reload();
        }
      });
  },
};
</script>

<style lang="scss">
@import "./style.scss";
</style>
