<template>
  <div class="flex column justify-center text-center text-body1">
    <p>Upload image</p>
    <q-file
      outlined
      clearable
      v-model="fileName"
      class="q-mb-md"
      label="Browse files..."
      accept=".jpg, image/*"
      @input="handleFile"
    />
    <p>Click the image to start editing</p>
    <div id="display-area">
      <div
        class="container cursor-pointer column items-center"
        @mouseover="showOverlay = !showOverlay"
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
      ref="popup"
      anchor="center middle"
      self="center left"
      transition-show="scale"
      transition-hide="scale"
      target="#display-area"
    >
      <CropperDialog
        v-on:destroy="finishCropper"
        :imageSrc="imageSrc"
      />
    </q-popup-proxy>
    <Links />
  </div>
</template>

<script>
import CropperDialog from './CropperDialog'
import Links from './Links'

export default {
  name: 'Displayer',

  data () {
    return {
      imageSrc: 'https://upload.wikimedia.org/wikipedia/commons/a/a4/Ada_Lovelace_portrait.jpg',
      showOverlay: false,
      fileName: null
    }
  },

  methods: {
    handleFile (file) {
      this.imageSrc = URL.createObjectURL(file)
    },

    finishCropper (croppedImage) {
      // console.log(croppedImage)
      this.imageSrc = croppedImage
    }
  },

  components: {
    CropperDialog,
    Links
  }
}
</script>

<style lang="stylus" scoped>
  .container
    position relative
    max-width 80vw
    max-height 50vh
    overflow hidden
  .container img
    display block
    max-width 100%
    max-height 50vh
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
