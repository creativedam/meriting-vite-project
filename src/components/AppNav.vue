<template>
  <nav class="mini-menu" aria-label="Primary navigation">
    <RouterLink to="/">Home</RouterLink>
    <RouterLink to="/contact">Contact</RouterLink>
    <RouterLink to="/appointments">Appointments</RouterLink>
  </nav>
</template>

<style scoped>
.mini-menu {
  display: flex;
  justify-content: flex-end;
  gap: 0.75rem;
}

.mini-menu a {
  padding: 0.45rem 0.7rem;
  border: 1px solid #d7ead9;
  border-radius: 6px;
  color: #14532d;
  font-size: 0.9rem;
  font-weight: 800;
}

.mini-menu a:hover,
.mini-menu a.router-link-active {
  border-color: #19b10d;
  background: #19b10d;
  color: #ffffff;
}

@media (max-width: 560px) {
  .mini-menu {
    justify-content: flex-start;
    overflow-x: auto;
  }
}
</style>
