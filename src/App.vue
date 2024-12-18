<template>
  <v-app>
    <v-main>
      <router-view />
    </v-main>
  </v-app>
</template>

<script setup>
  //
</script>

<style lang="scss" scoped>
@font-face {
  font-family: "Silkscreen";
  src: local("Silkscreen"),   url(./assets/fonts/Silkscreen/slkscr.ttf) format("truetype");}

:deep(.v-main) {
  --v-layout-bottom: 0px !important;
}
</style>