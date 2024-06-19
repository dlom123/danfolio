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
          <span class="title text-green">Chompy</span>
        </template>

        <!-- Only embed the thumbnail in the project info section for xs/sm viewports -->
        <template v-if="smAndDown" #image>
          <Thumbnail :src="project.imageThumbnail" :galleryImages="project.otherImages" />
        </template>

        <template #description>
          <p class="mb-2 mb-md-4">
          </p>
        </template>

        <template #chips>
          <ChipPython />
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
import img2 from './images/02.png'
import img3 from './images/03.png'
import img4 from './images/04.png'

const props = defineProps({
  flipped: {
    type: Boolean,
    default: false,
  },
})

const { smAndDown } = useDisplay()

const projectImages = [img1, img2, img3, img4]
const project = {
  title: 'Chompy',
  subtitle: 'Treacherous letter-guessing game.',
  description: [
    'Guess the missing letters correctly to avoid plunging into the Chompster\'s chompers!',
    'No story has ever been told of what lies beneath!',
    `
      <div class="border-sm pa-2">
        <div class="mb-2">Try it out!</div>
        <code>
          ssh 157.245.213.39 -o PubkeyAuthentication=no -l chompy
        </code>
        <div class="mt-4 mb-1">Password</div>
        <code>chomp!</code>
      </div>
    `,
  ],
  repoPrimary: {
    title: 'Chompy',
    url: 'https://github.com/dlom123/chompy',
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