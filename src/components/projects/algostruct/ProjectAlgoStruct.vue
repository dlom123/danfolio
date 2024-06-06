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
          <span class="title1 text-white">Algo</span>
          <span class="title2 text-light-blue">Struct</span>
        </template>

        <!-- Only embed the thumbnail in the project info section for xs/sm viewports -->
        <template v-if="smAndDown" #image>
          <Thumbnail :src="project.imageThumbnail" :galleryImages="project.otherImages" />
        </template>

        <!-- <template #description>
          <p class="mb-2 mb-md-4">
            An interactive computer science playground that allows you to step through algorithms visually,
            while outlining the steps and code involved along the way.
          </p>
          <p class="mb-2 mb-md-4">
            Created as my final project for the online <a href="https://cs50.harvard.edu/x/2020/">Harvard CS50x</a>
            course.
          </p>
        </template> -->

        <template #chips>
          <ChipVue version="2" />
          <ChipVuetify />
          <ChipSass />
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
import { useDisplay } from 'vuetify'

import imageThumbnail from './images/tn.png'
import img1 from './images/01.png'
import img2 from './images/02.png'
import img3 from './images/03.png'
import img4 from './images/04.png'
import img5 from './images/05.png'
import img6 from './images/06.png'
import img7 from './images/07.png'
import img8 from './images/08.png'

const props = defineProps({
  flipped: {
    type: Boolean,
    default: false,
  },
})

const { smAndDown } = useDisplay()

const projectImages = [img1, img2, img3, img4, img5, img6, img7, img8]
const project = {
  title: 'AlgoStruct',
  subtitle: 'Computer science learning tool.',
  description: [
    `An interactive computer science playground that allows you to step through algorithms visually,
    while outlining the steps and code involved along the way.`,
    `Created as my final project for the online
    <a href="https://cs50.harvard.edu/x/2020/" target="_blank">Harvard CS50x</a> course.`,
  ],
  repoPrimary: {
    title: 'AlgoStruct',
    url: 'https://github.com/dlom123/algostruct',
    demoUrl: '',
  },
  otherRepos: [],
  imageThumbnail,
  otherImages: [],
}

onMounted(() => {
  console.log('HEY')
  // preload project images in order to get their width for use in the image gallery
  projectImages.forEach(projectImage => {
    const img = new Image()
    img.src = projectImage
    project.otherImages.push(img)
  })
})
</script>

<style lang="scss" scoped>
.title1 {
  -webkit-text-stroke-width: 1px;
  -webkit-text-stroke-color: lightblue;
}

.title2 {
  -webkit-text-stroke-width: 1px;
  -webkit-text-stroke-color: white;
}
</style>