<template>
  <div class="text-center">
    <v-dialog
      v-model="dialog"
      width="500"
    >
      <template v-slot:activator="{ on, attrs }">
        <v-btn class="info-btn mr-1 grey darken-3" position absolute bottom right fab v-bind="attrs" v-on="on"
          ><v-icon large>mdi-information-outline</v-icon></v-btn>
      </template>

      <v-card class="main-card">
        <v-card-title class="text-h5 grey darken-3 font-weight-bold">
          Can you break it?
        </v-card-title>

        <!-- <v-card-text class="py-2 text-subtitle-1">
          Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
        </v-card-text> -->

        <v-card-text class="tt py-2 text-subtitle-1">
          It's time for some brainstorming through interesting puzzles!.
          All the problems are timed overally, not indvidually. 
          Login with the UID and password provided in the credentials.
          You can submit answers multiple times. And once you submit, the question number (in navigation) will become blue
          indicating that you have attempted it.
        </v-card-text>

        <v-card-text class="tt py-2 font-weight-bold text-subtitle-1">
          Note that only your latest answer will be saved!
        </v-card-text>

        <v-divider></v-divider>

        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
            color="primary"
            text
            @click="dialog = false"
          >
            Perfect
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
export default {
  data(){
    return {
      dialog: false
    }
  },
};
</script>

<style scoped>

.tt{
  color: white !important;
}

.main-card{
  filter: brightness(60%);
}
.info-btn {
  /* position: absolute;
  right: 16px; */
  bottom: 95px !important;
}
.WordSection1 {
  font-family: "Lucida Sans", "Lucida Sans Regular", "Lucida Grande",
    "Lucida Sans Unicode", Geneva, Verdana, sans-serif;
}
</style>