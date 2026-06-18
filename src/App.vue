<script setup>
import SiteFooter from './components/SiteFooter.vue'
</script>

<template>
  <div class="app-shell">
    <RouterView />
    <SiteFooter />
  </div>
</template>

<style scoped>
.app-shell {
  width: 100%;
}
</style>
