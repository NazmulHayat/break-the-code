<template>
  <v-footer
    dark
    color="transparent"
    padless
    class="foot"
  > 
    <v-card
      flat
      tile
      color="transparent"
      class="crd white--text text-center"
    >
    <v-divider></v-divider>

    <v-card-text class="">
      <strong class="font-weight-bold text-md-subtitle-1 text-subtitle-2"> PIHACKS'21 </strong> 
      <v-icon class="pb-1 mx-2" type="button" onclick="window.open('https://www.facebook.com/events/341277440774977/?active_tab=discussion', '_blank')"> mdi-gmail </v-icon>
      <v-icon class="pb-1 mx-2" type="button" onclick="window.open('https://www.facebook.com/events/341277440774977/?active_tab=discussion', '_blank')"> mdi-facebook </v-icon>
      <v-icon class="pb-1 mx-2" type="button" onclick="window.open('https://www.instagram.com/pihacks21/', '_blank')"> mdi-instagram </v-icon>
    </v-card-text>

    <strong class="mb-4 text-md-subtitle-1 text-subtitle-2"> BREAK-THE-CODE |  Developed by Nazmul Hayat and Raiyan Md. Shah</strong> 
    </v-card> 
  </v-footer>
</template>

<script>
  export default {
    data: () => ({
      
    }),
  }
</script>

<style scoped>
  .crd{
    width: 100vw;
  }

  .v-card__subtitle, .v-card__text, .v-card__title {
    padding-top: 8px !important;
    padding-bottom: 4px !important;
  }

</style>