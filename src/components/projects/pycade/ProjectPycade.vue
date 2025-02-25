<template>
  <v-row class="px-4">
    <!-- BEGIN left-side image -->
    <v-col v-if="!smAndDown && !flipped" cols="12" md="6" class="align-self-start">
      <Thumbnail :src="project.imageThumbnail" :galleryImages="project?.otherImages" />
    </v-col>
    <!-- END left-side image -->

    <!-- BEGIN project info -->
    <v-col cols="12" md="6">
      <ProjectInfo :project="project">
        <template #title>
          <span class="title text-green">Pycade</span>
        </template>

        <!-- Only embed the thumbnail in the project info section for xs/sm viewports -->
        <template v-if="smAndDown" #image>
          <Thumbnail :src="project.imageThumbnail" :galleryImages="project?.otherImages" />
        </template>

        <template #chips>
          <ChipPython />
          <ChipSQLite />
        </template>
      </ProjectInfo>
    </v-col>
    <!-- END project info -->

    <!-- BEGIN right-side image -->
    <v-col v-if="!smAndDown && flipped" cols="12" md="6" class="align-self-start">
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
import img9 from './images/09.png'
import img10 from './images/10.png'
import img11 from './images/11.png'
import img12 from './images/12.png'
import img13 from './images/13.png'
import img14 from './images/14.png'
import img15 from './images/15.png'
import img16 from './images/16.png'

defineProps({
  flipped: {
    type: Boolean,
    default: false,
  },
})

const { smAndDown } = useDisplay()

const projectImages = [img1, img2, img3, img4, img5, img6, img7, img8, img9, img10, img11, img12, img13, img14, img15, img16]
const project = {
  title: 'Pycade',
  subtitle: 'A keyboard arcade adventure.',
  description: [
    `A collaborative effort that I lead with my students during my time as a Python instructor.
    Browse the game gallery, play to earn tokens, and spend them on emojis in the Gift Shop to
    bedazzle your Leaderboard status!`,
  ],
  highlights: [
    'Collaborative group project that I led in an academic setting.',
    'Game programming concepts.',
    'Terminal-based user interface.',
  ],
  instructions: [
  `
      <div class="border-sm pa-4">
        <div class="mb-2">Try it out!</div>
        <code>
          ssh 157.245.213.39 -o PubkeyAuthentication=no -l pycade
        </code>
        <div class="mt-4 mb-1">Password</div>
        <code>play!</code>
      </div>
    `,
  ],
  repoPrimary: {
    title: 'Pycade',
    url: 'https://github.com/dlom123/pycade',
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
  font-family: 'monospace'
}
</style>