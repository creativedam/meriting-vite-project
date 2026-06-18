<script setup>
import ContactDetails from '../components/ContactDetails.vue'
import HomeHero from '../components/HomeHero.vue'
import Icon from '../components/Icon.vue'
import OpeningHours from '../components/OpeningHours.vue'
</script>

<template>
  <main class="contact-view">
    <HomeHero animated />

    <section class="contact-grid" aria-labelledby="contact-title">
      <div class="contact-card">
        <h2 id="contact-title">Contact Us</h2>
        <p>Book an appointment or ask our team for help with your reservation.</p>
        <ContactDetails />
        <a
          class="whatsapp-link"
          href="https://wa.me/26771450291"
          target="_blank"
          rel="noreferrer"
        >
          <Icon name="whatsapp" class="contact-action-icon" />
          Reach out to us on WhatsApp
        </a>
        <a class="phone-link" href="tel:+2673903660">
          <Icon name="telephone" class="contact-action-icon" />
          Call us on +267 390 3660
        </a>
      </div>

      <div class="contact-card">
        <OpeningHours />
      </div>
    </section>
  </main>
</template>

<style scoped>
.contact-view {
  padding: 2rem 1.5rem 0;
}

.contact-grid {
  display: grid;
  grid-template-columns: minmax(0, 1fr) minmax(280px, 0.8fr);
  gap: 1.5rem;
  width: min(1000px, 100%);
  margin: 3rem auto 0;
  text-align: left;
}

.contact-card {
  display: grid;
  align-content: start;
  gap: 1rem;
  padding: 1.5rem;
  border: 1px solid #d7ead9;
  border-radius: 8px;
  background: #f7fff8;
}

h2 {
  margin: 0;
  color: #14532d;
  font-size: 1.6rem;
}

p {
  margin: 0;
  color: #4b5563;
}

.contact-card :deep(.contact-details) {
  justify-content: flex-start;
}

.whatsapp-link,
.phone-link {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 0.6rem;
  width: fit-content;
  padding: 0.8rem 1rem;
  border-radius: 6px;
  color: #ffffff;
  font-weight: 800;
}

.whatsapp-link {
  background: #19b10d;
}

.phone-link {
  background: #005ee4;
}

.contact-action-icon {
  width: 24px;
  height: 24px;
}

@media (max-width: 760px) {
  .contact-grid {
    grid-template-columns: 1fr;
  }
}
</style>
