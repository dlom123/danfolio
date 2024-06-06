<template>
  <v-chip variant="flat" color="#42b883" size="small" class="font-weight-bold">
    Vue.js<span v-if="version">&nbsp;{{ version }}</span>
  </v-chip>
</template>

<script setup>
defineProps(['version'])
</script>