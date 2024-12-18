<template>
    <v-col cols="12">
      <v-card class="pa-4">
        <ProjectInfoSmall :project="project">
          <template #title>
            <span
              v-for="(char, i) in project.title.split('')"
              :key="i"
              class="title"
              :style="{color: titleColors[i]}"
            >
              {{ char }}
            </span>
          </template>

          <template #chips>
            <ChipOther label="x86 Assembly" inverted />
          </template>
        </ProjectInfoSmall>
      </v-card>
    </v-col>
</template>

<script setup>
defineProps({
  flipped: {
    type: Boolean,
    default: false,
  },
})

// colors from the CGA color palette that PixelDraw would have used
const titleColors = [
  '#0000aa', // blue
  '#00aa00', // green
  '#00aaaa', // cyan
  '#aa0000', // red
  '#aa00aa', // magenta
  '#aa5500', // brown
  '#aaaaaa', // light grey
  '#555555', // dark grey
  '#5555ff', // light blue
]
const project = {
  title: 'PixelDraw',
  subtitle: 'Etch A Sketch!',
  description: [
    'Draw on the screen pixel-by-pixel.'
  ],
  repoPrimary: {
    title: 'PixelDraw',
    url: 'https://github.com/dlom123/once-upon-a-time/blob/main/pixeldraw',
    demoUrl: '',
  },
  otherRepos: [],
  otherImages: [],
  isResponsive: false,
}
</script>

<style lang="scss" scoped>
.title {
  font-family: "Silkscreen", Helvetica, Arial;
  -webkit-text-stroke-width: 0.5px;
  -webkit-text-stroke-color: white;
}
</style>