<template>
  <v-main class="gradiente-bg">
    <router-view />
    <PageFooter />
  </v-main>
</template>

<script>
import PageFooter from '@/components/PageFooter.vue'

export default {
  data: () => ({}),
  components: {
    PageFooter,
  },
}
</script>

<style scoped></style>
