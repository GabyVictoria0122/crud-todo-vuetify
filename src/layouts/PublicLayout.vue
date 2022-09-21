<template>
  <div class="gradiente-bg">
    <router-view />
    <PageFooter />
  </div>
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
