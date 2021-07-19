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
    <v-card-text>
      <strong class="mt-4 text-md-subtitle-1 text-subtitle-2"> Developed by Nazmul Hayat and Raiyan Md. Shah</strong>
    </v-card-text>

    <v-card-text class="pb-2">
      <strong class="text-md-subtitle-1 text-subtitle-2"> Copyright © 2021 PIHACKS | BREAK-THE-CODE</strong> 
      <v-icon class="pb-1 ml-3" type="button" onclick="window.open('https://www.facebook.com/events/341277440774977/?active_tab=discussion', '_blank')"> mdi-facebook </v-icon>
      <v-icon class="pb-1 ml-2" type="button" onclick="window.open('https://www.instagram.com/pihacks21/', '_blank')"> mdi-instagram </v-icon>
    </v-card-text>



      <!-- <v-card-text class="white--text pt-0">
        Phasellus feugiat arcu sapien, et iaculis ipsum elementum sit amet. Mauris cursus commodo interdum. Praesent ut risus eget metus luctus accumsan id ultrices nunc. Sed at orci sed massa consectetur dignissim a sit amet dui. Duis commodo vitae velit et faucibus. Morbi vehicula lacinia malesuada. Nulla placerat augue vel ipsum ultrices, cursus iaculis dui sollicitudin. Vestibulum eu ipsum vel diam elementum tempor vel ut orci. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus.
      </v-card-text> -->
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