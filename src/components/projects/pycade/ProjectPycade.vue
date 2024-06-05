<template>
  <v-row class="px-4">
    <!-- BEGIN left-side image -->
    <v-col v-if="!smAndDown && !flipped" cols="12" md="6" class="align-self-end">
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

const props = defineProps({
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
  repoPrimary: {
    title: 'Pycade',
    url: 'https://github.com/dlom123/pycade',
    demoUrl: '',
  },
  otherRepos: [],
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
  font-family: 'monospace'
}
</style>