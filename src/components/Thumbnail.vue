<template>
  <v-hover v-slot="{ isHovering, props }">
    <v-img v-bind="props" :src="src" class="rounded border-md border-variant border-opacity-25">
      <v-overlay :model-value="isHovering" contained scrim="black" opacity="0.2"
        class="align-center justify-center cursor-pointer" @click="openGallery">
        <v-icon icon="mdi-image-multiple" size="x-large" color="secondary"></v-icon>
      </v-overlay>
    </v-img>
  </v-hover>

  <v-overlay v-model="showGallery" width="100%" height="100vh" scrim="black" opacity="0.8"
    @afterLeave="handleAfterLeaveGallery">
    <v-carousel :model-value="currentImage" :show-arrows="galleryImages.length > 1 ? 'hover' : false"
      hide-delimiter-background :hide-delimiters="!(galleryImages.length > 1)" theme="light" style="height: 100vh;">
      <template #prev>
        <v-btn icon="mdi-chevron-left" @click.stop="handleClickPrev" />
      </template>

      <v-carousel-item v-for="(image, i) in galleryImages" :key="i">
        <div class="d-flex align-center" style="height: 100%;">
          <v-img :src="image" :max-width="image.width" max-height="950" class="mx-auto" @click.stop />
        </div>
      </v-carousel-item>

      <template #next>
        <v-btn icon="mdi-chevron-right" @click.stop="handleClickNext" />
      </template>
    </v-carousel>

    <v-btn icon="mdi-close" class="btn-close" @click="handleCloseGallery" />
  </v-overlay>
</template>

<script setup>
import { ref } from 'vue'

const props = defineProps({
  galleryImages: Array,
  onClick: Function,
  src: String,
})

const currentImage = ref(0)
const showGallery = ref(false)

function handleAfterLeaveGallery() {
  currentImage.value = 0
}

function handleClickNext() {
  currentImage.value = (currentImage.value === (props.galleryImages.length - 1)) ? 0 : currentImage.value + 1
}

function handleClickPrev() {
  currentImage.value = (currentImage.value === 0) ? props.galleryImages.length - 1 : currentImage.value - 1
}

function handleCloseGallery() {
  showGallery.value = false
  currentImage.value = 0
}

function openGallery() {
  showGallery.value = true
}
</script>

<style lang="scss" scoped>
.btn-close {
  position: absolute;
  top: 20px;
  right: 40px;
}
</style>