<template>
  <div class="wrapper column items-center no-scroll">
    <!-- <div class="row space-between no-wrap"> -->
    <div class="column items-center no-wrap">
      <div class="container">
        <img
          ref="image"
          :src="imageSrc"
          >
      </div>
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
    <q-btn
      label="OK"
      class="q-mt-sm"
      @click="finish(cropper, destination)"
    />
  </div>
</template>

<script>
import Cropper from 'cropperjs'
import 'cropperjs/dist/cropper.css'

export default {
  name: 'CropperDialog',

  data () {
    return {
      image: {},
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
    this.image = this.$refs.image
    const cropper = new Cropper(this.image, {
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
        this.destination = cropper.getCroppedCanvas().toDataURL('image/jpeg')
        this.preview = true
      }
    })
  },
  methods: {
    finish () {
      // console.log(this.destination)
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
  .preview-container
    width 93%
    padding 2px
    margin-top 10px
    background-color #fff
    border-radius 3px
  .preview
    max-height 200px
</style>
