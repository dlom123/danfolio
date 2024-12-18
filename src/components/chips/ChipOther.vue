<template>
  <v-chip variant="flat" :color="inverted ? 'black' : 'grey'" size="small" class="font-weight-bold">
    {{ label }}
  </v-chip>
</template>

<script setup>
defineProps({
  inverted: {
    type: Boolean,
    default: false,
  },
  label: String,
})
</script>