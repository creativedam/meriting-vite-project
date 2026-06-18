<script setup>
import AppointmentActions from '../components/AppointmentActions.vue'
import BookingSteps from '../components/BookingSteps.vue'
import HomeHero from '../components/HomeHero.vue'
</script>

<template>
  <main class="home-view">
    <HomeHero animated />
    <AppointmentActions />
    <BookingSteps />
  </main>
</template>

<style scoped>
.home-view {
  padding: 2rem 1.5rem 0;
}
</style>
