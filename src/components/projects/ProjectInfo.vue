<template>
  <v-card variant="text" :subtitle="project.subtitle">
    <template #title>
      <h2 class="d-inline text-h4 font-weight-black">
        <slot v-if="$slots.title" name="title" />
        <span v-else>{{ project.title }}</span>
      </h2>
    </template>

    <slot name="image" />

    <template v-if="project?.repoPrimary?.demoUrl" #append>
      <v-btn color="primary" append-icon="mdi-open-in-new" :href="project?.repoPrimary?.demoUrl" target="_blank"
        class="text-capitalize">Try It Out!</v-btn>
    </template>

    <v-card-text class="rounded bg-surface-light pt-4 mt-4 mt-md-0">
      <p>Description...</p>
      <p>Description...</p>
      <p>Description...</p>
      <p>Description...</p>
      <p>Description...</p>
      <p>Description...</p>
      <p>Description...</p>
    </v-card-text>

    <v-card-actions class="bg-surface-light py-2 px-3 border-t-sm">
      <a :href="project.repoPrimary.url" target="_blank">
        <v-img src="@/assets/images/github-logo.png" width="32" />
      </a>
    </v-card-actions>
  </v-card>
</template>

<script setup>
defineProps({
  project: Object,
})
</script>

<style lang="scss" scoped>
.v-card {
  display: flex;
  flex-direction: column;
  height: 100%;
}

.v-card-text {
  overflow: auto;
}
</style>