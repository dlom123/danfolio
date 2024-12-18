<template>
  <v-container fluid class="pa-0">
    <v-row class="mt-6 mb-1 mb-md-4 justify-center">
      <v-col cols="auto" class="text-center">
        <h1 class="mb-4 text-h2 font-weight-bold">Daniel Lomelino</h1>
        <a href="mailto:dlomelino@pm.me">dlomelino@pm.me</a>
        <v-btn color="primary" size="small" prepend-icon="mdi-file-document-outline" :href="resume" target="_blank"
          class="text-capitalize ml-6">Resume</v-btn>
      </v-col>
    </v-row>

    <!-- BEGIN Projects section -->
    <v-row no-gutters>
      <v-col
        v-for="(projectComponent, i) in projectComponents"
        :key="i"
        cols="12"
        lg="10"
        offset-lg="1"
        xl="6"
        offset-xl="3"
      >

        <!-- BEGIN project -->
        <component :is="projectComponent" :flipped="!(i % 2)" class="my-6" />
        <!-- END project -->

        <v-divider v-if="i < projectComponents.length - 1" opacity="0.1" thickness="2" />
      </v-col>
    </v-row>
    <!-- END Projects section -->
    
    <v-divider opacity="0.5" thickness="2" />
    
    <!-- BEGIN Honorable Mentions section -->
    <v-row no-gutters class="py-8 bg-blue">
      <v-col cols="12" class="text-center">
        <h2 class="mb-4 text-h4">Honorable Mentions</h2>
      </v-col>

      <v-col
        v-for="(projectComponent, i) in projectHonorableMentions"
        :key="i"
        cols="12"
        sm="12"
        md="6"
        lg="5"
        :offset-lg="!(i % 2) ? 1 : 0"
        xl="3"
        :offset-xl="!(i % 2) ? 3 : 0"
        class="mt-0"
      >
        <component :is="projectComponent" />
      </v-col>
    </v-row>
    <!-- END Honorable Mentions section -->

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
import ProjectPixelDraw from '@/components/projects/honorable-mentions/ProjectPixelDraw'
import ProjectPycade from '@/components/projects/pycade/ProjectPycade'
import ProjectPyCandles from '@/components/projects/pycandles/ProjectPyCandles'
import ProjectTennis from '@/components/projects/tennis/ProjectTennis'
import resume from '@/assets/resume-daniel-lomelino.pdf'

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
const projectHonorableMentions = [
  ProjectPixelDraw,
]

function handleCloseOverlay() {
  currentImage.value = null
}
</script>