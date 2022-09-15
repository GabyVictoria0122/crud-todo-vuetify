<template>
  <v-toolbar class="light-blue white--text text-caption" dense>
    <v-app-bar-nav-icon class="white--text text-caption"></v-app-bar-nav-icon>

    <v-toolbar-title>Vuetodo</v-toolbar-title>

    <v-spacer></v-spacer>

    <v-btn icon class="white--text text-caption">
      <v-icon>fa-solid fa-magnifying-glass</v-icon>
    </v-btn>

    <v-btn icon class="white--text text-caption">
      <v-icon>fa-regular fa-face-grin-hearts</v-icon>
    </v-btn>

    <v-btn icon class="white--text text-caption" :to="{ name: 'home' }">
      <v-icon>fa-solid fa-ellipsis-vertical</v-icon>
    </v-btn>
  </v-toolbar>
</template>

<script>
import settings from '@/settings'

export default {
  data: () => ({
    version: settings.version,
    nodeEnv: settings.nodeEnv,
  }),
}
</script>
