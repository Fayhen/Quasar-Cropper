<template>
  <div class="flex column justify-center">
    <div>
      <div
        class="container cursor-pointer column items-center"
        @mouseover="showOverlay = !showOverlay"
        @click="renderCropper = !renderCropper"
      >
        <img
          ref="image"
          :src="imageSrc"
        >
        <div
          class="overlay flex justify-center items-center"
          :hidden="showOverlay"
        >
          <q-icon
            name="crop"
            size="xl"
            color="grey-10"
            class="crop-icon"
          />
        </div>
      </div>
    </div>
    <q-popup-proxy
      anchor="center middle"
      self="center left"
      transition-show="scale"
      transition-hide="scale"
    >
      <CropperDialog
        v-if="renderCropper"
        v-on:destroy="finishCropper"
        :imageSrc="imageSrc"
      />
    </q-popup-proxy>
  </div>
</template>

<script>
import CropperDialog from './CropperDialog'

export default {
  name: 'Displayer',

  data () {
    return {
      imageSrc: 'https://upload.wikimedia.org/wikipedia/commons/d/d5/Interior_of_Santi_Giovanni_e_Paolo_%28Venice%29_-_San_Domenico_e_San_Francesco%2C_di_Angelo_Lion.jpg',
      showOverlay: false,
      renderCropper: false
    }
  },

  methods: {
    finishCropper (croppedImage) {
      console.log(croppedImage)
      this.imageSrc = croppedImage
      this.renderCropper = false
    }
  },

  components: {
    CropperDialog
  }
}
</script>

<style lang="stylus" scoped>
  .container
    position relative
    width 80vw
    max-height 50vh
    overflow hidden
  .container img
    display block
    max-width 100%
    heigth 100%
  .container .overlay
    position absolute
    display flex
    top 0
    bottom 0
    left 0
    right 0
    width 100%
    height 100%
    background-color rgba(#fff, .7)
    opacity 0
    transition .3s ease
    &:hover
      opacity 0.6
  .crop-icon
    opacity 1
</style>
