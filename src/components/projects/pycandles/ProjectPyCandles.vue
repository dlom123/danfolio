<template>
  <v-row class="px-4">
    <!-- BEGIN left-side image -->
    <v-col v-if="!smAndDown && !flipped" cols="12" md="6" class="align-self-end">
      <Thumbnail :src="project.imageThumbnail" :galleryImages="project.otherImages" />
    </v-col>
    <!-- END left-side image -->

    <!-- BEGIN project info -->
    <v-col cols="12" md="6">
      <ProjectInfo :project="project">
        <template #title>
          <span class="title">PyCandles</span>
        </template>

        <!-- Only embed the thumbnail in the project info section for xs/sm viewports -->
        <template v-if="smAndDown" #image>
          <Thumbnail :src="project.imageThumbnail" :galleryImages="project.otherImages" />
        </template>

        <template #chips>
          <ChipPython />
          <ChipOther label="Yahoo! Finance API" />
        </template>
      </ProjectInfo>
    </v-col>
    <!-- END project info -->

    <!-- BEGIN right-side image -->
    <v-col v-if="!smAndDown && flipped" cols="12" md="6" class="align-self-end">
      <Thumbnail :src="project.imageThumbnail" :galleryImages="project?.otherImages" />
    </v-col>
    <!-- END right-side image -->
  </v-row>
</template>

<script setup>
import { useDisplay } from 'vuetify'

import imageThumbnail from './images/tn.png'
import img1 from './images/01.png'

const props = defineProps({
  flipped: {
    type: Boolean,
    default: false,
  },
})

const { smAndDown } = useDisplay()

const projectImages = [img1]
const project = {
  title: 'PyCandles',
  subtitle: 'Stock price visualizer.',
  description: [
    'Generate a candlestick chart of stock price activity over a given duration of time.'
  ],
  repoPrimary: {
    title: 'PyCandles',
    url: 'https://github.com/dlom123/pycandles',
    demoUrl: '',
  },
  otherRepos: [],
  imageThumbnail,
  otherImages: [],
  isResponsive: false,
}

onMounted(() => {
  // preload project images in order to get their width for use in the image gallery
  projectImages.forEach(projectImage => {
    const img = new Image()
    img.src = projectImage
    project.otherImages.push(img)
  })
})
</script>

<style lang="scss" scoped>
.title {
  text-shadow: 0 0 3px red, 0 0 5px orange;
}
</style>