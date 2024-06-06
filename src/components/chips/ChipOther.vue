<template>
  <v-chip variant="flat" color="grey" size="small" class="font-weight-bold">
    {{ label }}
  </v-chip>
</template>

<script setup>
defineProps(['label'])
</script>