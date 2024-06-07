<template>
  <v-card variant="text" :subtitle="project.subtitle" class="d-flex flex-column">
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

    <v-card-text class="rounded pa-2 mt-4 pa-md-4 pb-md-0 mt-md-0">
      <p v-for="(p, i) in project.description" :key="i" class="mb-2 mb-md-4" v-html="p" />
    </v-card-text>

    <v-card-actions class="py-2 px-3">
      <a :href="project.repoPrimary.url" target="_blank">
        <v-img src="@/assets/images/github-logo.png" width="32" />
      </a>
      <a v-if="project?.otherRepos.length" :href="project.otherRepos[0].url" target="_blank" class="ml-2">
        <v-img src="@/assets/images/github-logo.png" width="32" />
      </a>
      <v-row gutters="2">
        <v-col align="end" class="pa-0 ml-4">
          <slot v-if="$slots.chips" cols="12" name="chips" />
        </v-col>
      </v-row>
    </v-card-actions>
  </v-card>
</template>

<script setup>
defineProps({
  project: Object,
})
</script>