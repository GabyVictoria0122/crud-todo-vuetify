<template>
  <v-footer padless fixed app>
    <v-row no-gutters>
      <v-col class="light-blue pt-5 text-center white--text" cols="12">
        Copyright® {{ new Date().getFullYear() }} — <strong>Tasks</strong>
      </v-col>
      <v-col class="light-blue text-center white--text text-caption" cols="12">
        <strong>{{ version }}</strong> -
        {{ nodeEnv }}
        <p>
          <v-btn
            icon
            color="white"
            href="https://github.com/GabyVictoria0122?tab=repositories"
          >
            <v-icon>fa-brands fa-github</v-icon>
          </v-btn>
        </p>
      </v-col>
    </v-row>
  </v-footer>
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
