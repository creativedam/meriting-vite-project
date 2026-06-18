<script setup>
import Icon from './Icon.vue'
</script>

<template>
  <footer class="site-footer">
    <div class="footer-inner">
      <section>
        <h2>Gaborone Center</h2>
        <p>Carbo Centre, Plot 54518</p>
        <p>Gaborone, Botswana</p>
        <p>Tel: <a href="tel:+2673903660">+267 390 3660</a></p>
      </section>

      <section>
        <h2>Operating Hours</h2>
        <p>Monday-Friday 8 am-7 pm</p>
        <p>Saturday 8 am-6:30 pm</p>
        <p>Sunday Closed</p>
      </section>

      <section>
        <h2>Administration</h2>
        <p><a href="mailto:info@meriting.co.bw">info@meriting.co.bw</a></p>
        <p>Office 10 Meriting Medical Centre, Gaborone</p>
        <p><a href="tel:+2673903660">+267 390 3660</a></p>
      </section>

      <div class="footer-bottom">
        <Icon name="meriting-logo-grayscale" class="footer-logo" />
        <div class="social-links" aria-label="Social links">
          <a
            href="https://www.facebook.com/meritingclinic/"
            target="_blank"
            rel="noreferrer"
            aria-label="Facebook"
          >
            <Icon name="facebook" />
          </a>
          <a
            href="https://www.instagram.com/meritingmedicalcentre/"
            target="_blank"
            rel="noreferrer"
            aria-label="Instagram"
          >
            <Icon name="instagram" />
          </a>
        </div>
      </div>
    </div>
  </footer>
</template>

<style scoped>
.site-footer {
  margin-top: 7rem;
  background: #f4f5f7;
  color: #374151;
}

.footer-inner {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 3rem;
  width: min(1000px, 100%);
  margin: 0 auto;
  padding: 3rem 1.5rem 2rem;
  text-align: left;
}

h2 {
  margin: 0 0 1.25rem;
  color: #111111;
  font-size: 1rem;
  font-weight: 500;
}

p {
  margin: 0 0 0.5rem;
  color: #4b5563;
  font-size: 0.9rem;
  line-height: 1.45;
}

a {
  color: inherit;
}

a:hover {
  color: #005ee4;
}

.footer-bottom {
  display: flex;
  grid-column: 1 / -1;
  align-items: center;
  gap: 1.25rem;
  margin-top: 1rem;
  padding-top: 1.5rem;
  border-top: 1px solid #d9dde4;
}

.footer-logo {
  width: 150px;
}

.social-links {
  display: flex;
  gap: 0.75rem;
}

.social-links a {
  display: grid;
  place-items: center;
  width: 30px;
  height: 30px;
}

.social-links :deep(.icon) {
  width: 30px;
  height: 30px;
}

@media (max-width: 760px) {
  .site-footer {
    margin-top: 4rem;
  }

  .footer-inner {
    grid-template-columns: 1fr;
    gap: 2rem;
  }

  .footer-bottom {
    align-items: flex-start;
    flex-direction: column;
  }
}
</style>
