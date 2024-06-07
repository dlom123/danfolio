<template>
  <v-container fluid class="pa-0">
    <v-row class="mt-6">
      <v-col cols="12" class="text-center">
        <h1 class="text-h2 font-weight-bold">Daniel Lomelino</h1>
        <a href="mailto:dlomelino@pm.me">dlomelino@pm.me</a>
      </v-col>
    </v-row>

    <!-- BEGIN Projects section -->
    <v-row no-gutters>
      <v-col v-for="(projectComponent, i) in projectComponents" cols="12" lg="10" offset-lg="1" xl="6" offset-xl="3">

        <!-- BEGIN project -->
        <component :is="projectComponent" :flipped="!(i % 2)" class="my-6" />
        <!-- END project -->

        <v-divider v-if="i < projectComponents.length - 1" opacity="0.1" thickness="2" />
      </v-col>
    </v-row>
    <!-- END Projects section -->

    <v-overlay v-model="showOverlay" class="align-center justify-center" @afterLeave="handleCloseOverlay">
      <img :src="currentImage" class="image" />
    </v-overlay>
  </v-container>
</template>

<script setup>
import { ref } from 'vue'
import ProjectAlgoStruct from '@/components/projects/algostruct/ProjectAlgoStruct'
import ProjectChompy from '@/components/projects/chompy/ProjectChompy'
import ProjectCryptoDip from '@/components/projects/cryptodip/ProjectCryptoDip'
import ProjectCryptoverse from '@/components/projects/cryptoverse/ProjectCryptoverse'
import ProjectPycade from '@/components/projects/pycade/ProjectPycade'
import ProjectPyCandles from '@/components/projects/pycandles/ProjectPyCandles'
import ProjectTennis from '@/components/projects/tennis/ProjectTennis'

const showOverlay = ref(false)
const currentImage = ref(null)

const projectComponents = [
  ProjectCryptoDip,
  ProjectTennis,
  ProjectAlgoStruct,
  ProjectCryptoverse,
  ProjectChompy,
  ProjectPycade,
  ProjectPyCandles,
]
// const projects = [
//   { title: 'Chompy', repo: 'https://github.com/dlom123/chompy' },
//   { title: 'CryptoVerse', repo: 'https://github.com/dlom123/cryptoverse' },
//   { title: 'Danfolio', repo: 'https://github.com/dlom123/danfolio' },
//   { title: 'Music App', repo: 'https://github.com/danpunk/punk-app' },
//   { title: 'Music App API', repo: 'https://github.com/danpunk/punk-api' },
//   { title: 'Pycade', repo: 'https://github.com/dlom123/pycade' },
//   { title: 'PyCandle', repo: 'https://github.com/dlom123/candles' },
//   { title: 'Scanner App', repo: 'https://github.com/danpunk/punk-utils' },
//   { title: 'Tennis API', repo: 'https://github.com/dlom123/tennis-api' },
//   { title: 'Tennis App', repo: 'https://github.com/dlom123/tennis-app' },
// ]

function handleClickThumbnail(image) {
  currentImage.value = image
  showOverlay.value = true
}

function handleCloseOverlay() {
  currentImage.value = null
}
</script>