<template>
  <a :href="href" target="_blank">
    <v-chip size="small">
      <v-avatar start>
        <v-img src="@/assets/images/github-logo.png" width="32" />
      </v-avatar>
      {{ label }}
    </v-chip>
  </a>
</template>

<script setup>
import { useDisplay } from 'vuetify'

defineProps({
  href: String,
  label: String,
})

const { smAndDown } = useDisplay()
</script>