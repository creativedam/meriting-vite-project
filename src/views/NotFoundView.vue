<script setup>
import AppNav from '../components/AppNav.vue'
import Icon from '../components/Icon.vue'
</script>

<template>
  <main class="not-found-view">
    <header class="not-found-header">
      <RouterLink to="/" aria-label="Back to home">
        <Icon name="meriting-logo" class="not-found-logo" />
      </RouterLink>
      <AppNav />
    </header>

    <section class="not-found-panel" aria-labelledby="not-found-title">
      <p class="status-code">404</p>
      <h1 id="not-found-title">Page Not Found</h1>
      <p>
        The page you are looking for is unavailable or may have moved. You can
        return home and continue from there.
      </p>
      <RouterLink class="home-button" to="/">Back to Home</RouterLink>
    </section>
  </main>
</template>

<style scoped>
.not-found-view {
  display: grid;
  gap: 3rem;
  width: min(1020px, 100%);
  margin: 0 auto;
  padding: 2rem 1.5rem 0;
}

.not-found-header {
  display: grid;
  grid-template-columns: auto auto;
  align-items: center;
  justify-content: space-between;
  gap: 1rem;
}

.not-found-logo {
  width: 150px;
}

.not-found-panel {
  display: grid;
  justify-items: center;
  gap: 1rem;
  padding: 4rem 1.5rem;
  border: 1px solid #d7ead9;
  border-radius: 8px;
  background: #f7fff8;
  text-align: center;
}

.status-code {
  margin: 0;
  color: #19b10d;
  font-size: clamp(3rem, 10vw, 6rem);
  font-weight: 900;
  line-height: 1;
}

h1 {
  margin: 0;
  color: #26334a;
  font-size: clamp(2rem, 5vw, 3.25rem);
}

.not-found-panel p:not(.status-code) {
  max-width: 560px;
  margin: 0;
  color: #4b5563;
  font-size: 1.05rem;
}

.home-button {
  display: inline-flex;
  justify-content: center;
  margin-top: 1rem;
  padding: 1rem 2.5rem;
  border-radius: 8px;
  background: #19b10d;
  color: #ffffff;
  font-size: 1.15rem;
  font-weight: 900;
}

.home-button:hover {
  background: #128b09;
  color: #ffffff;
}

@media (max-width: 760px) {
  .not-found-header {
    grid-template-columns: 1fr;
    justify-items: start;
  }
}
</style>
