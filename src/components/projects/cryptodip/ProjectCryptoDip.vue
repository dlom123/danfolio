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
          <span class="text-blue">Crypto</span>
          <span class="text-red">Dip</span>
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
          <ChipOther label="CoinMarketCap API" />
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

const props = defineProps({
  flipped: {
    type: Boolean,
    default: false,
  },
})

const { smAndDown } = useDisplay()

const projectImages = [img1, img2, img3, img4, img5, img6]
const project = {
  title: 'CryptoDip',
  subtitle: 'Portfolio management app for the opportunistic.',
  description: [
    `A privacy-first, wallet aggregation tool geared toward maximizing investment decisions. All
    data must be entered manually, is stored only in the browser, and is never sent over the network.`,
  ],
  repoPrimary: {
    title: 'App',
    url: 'https://github.com/dlom123/cryptodip',
    demoUrl: 'https://cryptodip.app',
  },
  otherRepos: [
    {
      title: 'API',
      url: 'https://github.com/dlom123/cryptodip-api',
    },
  ],
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