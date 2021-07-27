<template>
  <v-footer dark color="transparent" padless class="foot">
    <v-card flat tile color="transparent" class="crd white--text text-center">
      <v-divider></v-divider>

      <v-card-text class="asd">
        <strong class="font-weight-bold text-md-h6 text-subtitle-2">
          PIHACKS'21
        </strong>
        <v-icon
          class="pb-0 mx-2"
          type="button"
          onclick="window.open('mailto:pihacks21@gmail.com', '_blank')"
        >
          mdi-gmail
        </v-icon>
        <v-icon
          class="pb-0 mx-2"
          type="button"
          onclick="window.open('https://www.facebook.com/events/341277440774977/?active_tab=discussion', '_blank')"
        >
          mdi-facebook
        </v-icon>
        <v-icon
          class="pb-0 mx-2"
          type="button"
          onclick="window.open('https://www.instagram.com/pihacks21/', '_blank')"
        >
          mdi-instagram
        </v-icon>
      </v-card-text>

      <strong class="text-md-h6 text-subtitle-2">
        BREAK-THE-CODE | Developed by Nazmul Hayat and Raiyan Md. Shah</strong
      >
    </v-card>
  </v-footer>
</template>

<script>
export default {
  data: () => ({}),
};
</script>

<style scoped>
@font-face {
  font-family: fkpieceofshit;
  src: url("../assets/VCR_OSD_MONO.ttf");
}

.v-application .text-md-h6 {
  font-family: "fkpieceofshit" !important;
  word-spacing: -2px;
}

.asd {
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: "fkpieceofshit" !important;
}

.crd {
  text-transform: uppercase;
  width: 100vw;
  margin: auto;
  font-family: "fkpieceofshit" !important;
}

.v-card__subtitle,
.v-card__text,
.v-card__title {
  padding-top: 8px !important;
  padding-bottom: 4px !important;
  font-family: "fkpieceofshit" !important;
}
</style>