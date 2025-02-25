<template>
  <v-card variant="text" class="d-flex flex-column">
    <template #title>
      <v-row no-gutters class="mb-2 justify-space-between align-center">
        <v-col cols="auto" class="pa-0">
          <h2 class="d-inline text-h4 font-weight-black">
            <slot v-if="$slots.title" name="title" />
            <span v-else>{{ project?.title }}</span>
          </h2>
        </v-col>
        <v-col v-if="showDemoButton" cols="auto" class="pa-0">
          <v-btn color="secondary" size="small" append-icon="mdi-open-in-new" :href="project?.repoPrimary?.demoUrl"
            target="_blank" class="text-capitalize">Try It Out!</v-btn>
        </v-col>
      </v-row>
    </template>

    <template #subtitle>
      <v-row no-gutters class="mb-2">
        <v-col cols="auto">
          {{ project?.subtitle }}
        </v-col>
      </v-row>
    </template>

    <slot name="image" />

    <v-card-text class="rounded pa-2 mt-2 mt-md-0">
      <p v-for="(p, i) in project?.description" :key="i" class="mb-2 mb-md-4" v-html="p" />
    </v-card-text>

    <v-card-text v-if="project?.highlights" class="rounded pa-2">
      <h4>Highlights</h4>
      <ul class="ml-4 mb-2 mb-md-4">
        <li v-for="(p, i) in project?.highlights" :key="i" v-html="p" />
      </ul>
    </v-card-text>

    <v-card-text v-if="project?.instructions" class="rounded pa-2 mt-2 mt-md-0">
      <p v-for="(p, i) in project?.instructions" :key="i" class="mb-2 mb-md-4" v-html="p" />
    </v-card-text>

    <v-card-actions>
      <v-row no-gutters>
        <v-col v-if="project?.otherRepos.length" cols="auto">
          <v-row no-gutters>
            <ChipRepo :label="project?.repoPrimary.title" :href="project?.repoPrimary.url" />
          </v-row>
          <v-row no-gutters>
            <ChipRepo :label="project?.otherRepos[0].title" :href="project?.otherRepos[0].url" />
          </v-row>
        </v-col>
        <v-col v-else cols="auto">
          <a :href="project?.repoPrimary.url" target="_blank">
            <v-img src="@/assets/images/github-logo.png" width="32" />
          </a>
        </v-col>

        <v-col align="end" class="pa-0 ml-4">
          <slot v-if="$slots.chips" cols="12" name="chips" />
        </v-col>
      </v-row>
    </v-card-actions>
  </v-card>
</template>

<script setup>
import { computed } from 'vue'
import { useDisplay } from 'vuetify'

const props = defineProps({
  project: Object,
})

const { mobile, mdAndUp } = useDisplay()

const showDemoButton = computed(() => (
  !!props.project?.repoPrimary?.demoUrl
  && (
    mdAndUp.value
    || (mobile.value && props.project?.isResponsive)
  )
)
)
</script>

<style lang="scss" scoped>
:deep(.v-card-item) {
  padding: 0;
}
</style>