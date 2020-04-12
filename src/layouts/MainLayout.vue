<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          :icon="fabGithub"
        >
          <q-tooltip content-class="bg-secondary">See repository</q-tooltip>
        </q-btn>

        <q-toolbar-title>
          Quasar Cropper
        </q-toolbar-title>

        <div>Quasar v{{ $q.version }}</div>
      </q-toolbar>
    </q-header>

    <q-page-container class="flex justify-center window-height">
      <Displayer />
    </q-page-container>
  </q-layout>
</template>

<script>
import Displayer from 'components/Displayer'
import { fabGithub } from '@quasar/extras/fontawesome-v5'

export default {
  name: 'MainLayout',

  created () {
    this.fabGithub = fabGithub
  },

  components: {
    Displayer
  }
}
</script>
