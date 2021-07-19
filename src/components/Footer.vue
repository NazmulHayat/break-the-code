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
      <strong class="text-md-subtitle-1 text-subtitle-2"> PIHACKS 2021 | BREAK-THE-CODE </strong> 
      <v-icon class="pb-1 ml-4" type="button" onclick="window.open('https://www.facebook.com/events/341277440774977/?active_tab=discussion', '_blank')"> mdi-facebook </v-icon>
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
</style>