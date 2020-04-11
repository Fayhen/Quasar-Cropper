<template>
  <div class="wrapper column items-center no-scroll">
    <!-- <div class="row space-between no-wrap"> -->
    <div class="column items-center no-wrap">
      <div
        class="row justify-between no-wrap q-mb-md"
        style="width: 93%"
      >
        <q-btn
          round
          icon="rotate_left"
          color="primary"
          @click="rotateLeft()"
        >
          <q-tooltip content-class="bg-secondary">Rotate left</q-tooltip>
        </q-btn>
        <q-btn
          round
          icon="rotate_right"
          color="primary"
          @click="rotateRight()"
        >
          <q-tooltip content-class="bg-secondary">Rotate right</q-tooltip>
        </q-btn>
        <q-btn
          round
          icon="settings_backup_restore"
          color="primary"
          @click="resetCropper()"
        >
          <q-tooltip content-class="bg-secondary">Reset</q-tooltip>
        </q-btn>
        <q-btn
          round
          icon="close"
          color="primary"
          v-close-popup
        >
          <q-tooltip content-class="bg-secondary">Cancel</q-tooltip>
        </q-btn>
        <q-btn
          round
          icon="done"
          color="primary"
          @click="finish()"
          v-close-popup
        >
          <q-tooltip content-class="bg-secondary">Crop and finish</q-tooltip>
        </q-btn>
      </div>
      <div class="container">
        <img
          ref="image"
          :src="imageSrc"
          >
      </div>
      <p class="q-mt-md text-weight-bold">Preview:</p>
      <div
        v-if="preview"
        class="preview-container column items-center"
      >
        <img
          class="preview"
          :src="destination"
        >
      </div>
      <div
        v-else
        class="preview column items-center"
      >
        Loading cropper...
        <q-spinner
          size="3em"
          color="primary"
        />
      </div>
    </div>
  </div>
</template>

<script>
import Cropper from 'cropperjs'
import 'cropperjs/dist/cropper.css'

export default {
  name: 'CropperDialog',

  data () {
    return {
      cropper: {},
      destination: {},
      preview: false
    }
  },

  props: {
    imageSrc: {
      type: [String, Object]
    }
  },

  mounted () {
    this.startCropper()
  },

  methods: {
    startCropper () {
      this.cropper = new Cropper(this.$refs.image, {
        viewMode: 1,
        aspectRatio: 1 / 1,
        crop: () => {
          // console.log(event.detail.x)
          // console.log(event.detail.y)
          // console.log(event.detail.width)
          // console.log(event.detail.height)
          // console.log(event.detail.rotate)
          // console.log(event.detail.scaleX)
          // console.log(event.detail.scaleY)
          this.destination = this.cropper.getCroppedCanvas().toDataURL('image/jpeg')
          this.preview = true
        }
      })
    },

    destroyCropper () {
      this.cropper.destroy()
    },

    resetCropper () {
      this.cropper.reset()
    },

    rotateLeft () {
      this.cropper.rotate(-90)
    },

    rotateRight () {
      this.cropper.rotate(90)
    },

    finish () {
      this.$emit('destroy', this.destination)
    }
  }

}
</script>

<style lang="stylus" scoped>
  .wrapper
    max-width 80vw
    padding 10px
    @media screen and (min-width: 500px) {
      max-width 50vw
      @media screen and (min-width: 800px) {
        max-width 30vw
      }
    }
    background-color rgb(230, 230, 230)
  .container
    width 93%
    margin 3px
  .container img
    display block
    max-width 100%
    max-height 400px
  .preview-container
    width 93%
    padding 2px
    background-color #fff
    border-radius 3px
  .preview
    max-height 200px
</style>
