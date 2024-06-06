<template>
  <v-row class="px-4">
    <!-- BEGIN left-side image -->
    <v-col v-if="!smAndDown && !flipped" cols="12" md="6">
      <Thumbnail :src="project.imageThumbnail" :galleryImages="project.otherImages" />
    </v-col>
    <!-- END left-side image -->

    <!-- BEGIN project info -->
    <v-col cols="12" md="6">
      <ProjectInfo :project="project">
        <template #title>
          <span class="title">Tennis!</span>
        </template>

        <!-- Only embed the thumbnail in the project info section for xs/sm viewports -->
        <template v-if="smAndDown" #image>
          <Thumbnail :src="project.imageThumbnail" :galleryImages="project.otherImages" />
        </template>

        <template #chips>
          <ChipVue version="2" />
          <ChipVuetify />
          <ChipSass />
          <ChipDocker />
          <ChipOther label="REST API" />
          <ChipPostgreSQL />
        </template>
      </ProjectInfo>
    </v-col>
    <!-- END project info -->

    <!-- BEGIN right-side image -->
    <v-col v-if="!smAndDown && flipped" cols="12" md="6">
      <Thumbnail :src="project.imageThumbnail" :galleryImages="project?.otherImages" />
    </v-col>
    <!-- END right-side image -->
  </v-row>
</template>

<script setup>
import { onMounted } from 'vue'
import { useDisplay } from 'vuetify'

import ProjectInfo from '@/components/projects/ProjectInfo.vue'
import Thumbnail from '@/components/Thumbnail'

import imageThumbnail from './images/tn.png'
import img1 from './images/01.png'
import img2 from './images/02.png'
import img3 from './images/03.png'
import img4 from './images/04.png'
import img5 from './images/05.png'
import img6 from './images/06.png'

const props = defineProps({
  flipped: {
    type: Boolean,
    default: false,
  },
})

const { smAndDown } = useDisplay()

const projectImages = [img1, img2, img3, img4, img5, img6]
const project = {
  title: 'Tennis!',
  subtitle: 'Tennis management tool.',
  description: [
    'An app for managing tennis matches and gathering and analyzing stats.'
  ],
  repoPrimary: {
    title: 'Tennis App',
    url: 'https://github.com/dlom123/tennis-app',
    demoUrl: '',
  },
  otherRepos: [
    {
      title: 'Tennis API',
      url: 'https://github.com/dlom123/tennis-api',
      demoUrl: '',
    },
  ],
  imageThumbnail,
  otherImages: [],
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
  -webkit-text-stroke-width: 1px;
  -webkit-text-stroke-color: green;
}
</style>