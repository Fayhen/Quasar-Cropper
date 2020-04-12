<template>
  <div class="text-center text-body1">

    <p class="q-mt-md q-mb-none">Powered by:</p>

    <div class="row justify-between no-wrap">

      <a
        href="https://quasar.dev/"
        target="_blank"
        rel="noopener noreferrer"
      >
        <div>
          <img
            src="statics/app-logo-128x128.png"
            alt="Quasar Framework logo"
            class="link-container"
          >
          <p class="text-caption">Quasar Framework</p>
          <q-tooltip content-class="bg-secondary">Click to visit</q-tooltip>
        </div>
      </a>

      <a
        href="https://vuejs.org/"
        target="_blank"
        rel="noopener noreferrer"
      >
        <div>
          <img
            src="https://vuejs.org/images/logo.png"
            alt="Vue.js logo"
            class="link-container"
          >
          <p class="text-caption">Vue.js</p>
          <q-tooltip content-class="bg-secondary">Click to visit</q-tooltip>
        </div>
      </a>

      <a
        href="https://fengyuanchen.github.io/cropperjs/"
        target="_blank"
        rel="noopener noreferrer"
        class="self-stretch flex column justify-between no-wrap"
      >
        <div class="fit flex column justify-center">
          <div class="cropper-logo">
            <p class="q-ml-sm q-mr-sm">Cropper.js</p>
          </div>
        </div>
        <p class="text-caption">Cropper.js</p>
        <q-tooltip content-class="bg-secondary">Click to visit</q-tooltip>
      </a>

    </div>
  </div>
</template>

<script>
export default {
  name: 'Links'
}
</script>

<style lang="stylus" scoped>
  a
    color inherit
    text-decoration none
  .link-container
    width 64px
    height 64px
  .cropper-logo
    height 32px
    background-color #007BFF
    color #FFF
    border-radius 2px
    line-height 32px
</style>
