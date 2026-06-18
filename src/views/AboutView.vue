<script setup>
import AppNav from '../components/AppNav.vue'
import ContactDetails from '../components/ContactDetails.vue'
import Icon from '../components/Icon.vue'
import OpeningHours from '../components/OpeningHours.vue'
</script>

<template>
  <main class="about-view">
    <header class="about-header">
      <RouterLink to="/" aria-label="Back to home">
        <Icon name="meriting-logo-grayscale" class="about-logo" />
      </RouterLink>
      <AppNav />
    </header>
    <h1>Meriting Medical Centre</h1>
    <p>Quality care, clear communication, and simple access to medical services.</p>
    <section class="contact-panel" aria-labelledby="contact-heading">
      <div class="contact-section">
        <h2 id="contact-heading">Contact</h2>
        <ContactDetails />
      </div>
      <OpeningHours />
    </section>
  </main>
</template>

<style scoped>
.about-view {
  display: grid;
  gap: 1rem;
  justify-items: center;
  padding: 2rem 1.5rem 0;
}

.about-header {
  display: grid;
  grid-template-columns: auto auto;
  align-items: center;
  justify-content: space-between;
  gap: 1rem;
  width: min(1020px, 100%);
}

.about-logo {
  width: 150px;
}

h1 {
  margin: 0;
  font-size: clamp(2rem, 6vw, 3.25rem);
}

p {
  max-width: 560px;
  margin: 0;
  color: #4b5563;
}

.contact-panel {
  display: grid;
  gap: 1.5rem;
  margin-top: 1rem;
  padding: 1.25rem;
  border: 1px solid #d7ead9;
  border-radius: 8px;
  background: #f7fff8;
  width: min(560px, 100%);
}

.contact-section {
  display: grid;
  gap: 0.75rem;
}

h2 {
  margin: 0;
  color: #14532d;
  font-size: 1.25rem;
}

@media (max-width: 760px) {
  .about-header {
    grid-template-columns: 1fr;
    justify-items: start;
  }
}
</style>
