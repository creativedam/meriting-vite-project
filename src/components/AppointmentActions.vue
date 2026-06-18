<template>
  <section class="appointment-actions" aria-label="Appointment actions">
    <article class="action-card">
      <h2>Appointment Booking</h2>
      <strong>5</strong>
      <p>Active bookings</p>
      <RouterLink class="action-button action-button--green" to="/contact">
        + Book Appointment
      </RouterLink>
    </article>

    <article class="action-card">
      <h2>View Time Slots</h2>
      <strong>8</strong>
      <p>View available time slots</p>
      <RouterLink class="action-button action-button--blue" to="/appointments">
        + View Timeslots
      </RouterLink>
    </article>
  </section>
</template>

<style scoped>
.appointment-actions {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 2rem;
  width: min(1000px, 100%);
  margin: 4rem auto 0;
}

.action-card {
  display: grid;
  justify-items: center;
  padding: 1.8rem 1.35rem 1rem;
  border: 2px solid #064ada;
  border-radius: 8px;
  background: #ffffff;
}

h2 {
  margin: 0;
  color: #111111;
  font-size: 0.9rem;
  font-weight: 800;
  text-transform: uppercase;
}

strong {
  display: block;
  margin-top: 0.5rem;
  color: #2248b4;
  font-size: 3rem;
  line-height: 1;
}

p {
  margin: 0.25rem 0 0.6rem;
  color: #8a93a5;
  font-size: 0.8rem;
}

.action-button {
  display: block;
  width: 100%;
  padding: 0.7rem 1rem;
  border-radius: 6px;
  color: #ffffff;
  font-size: 1.05rem;
  font-weight: 800;
  line-height: 1;
  text-align: center;
}

.action-button--green {
  background: #19b10d;
}

.action-button--blue {
  background: #3369f4;
}

@media (max-width: 760px) {
  .appointment-actions {
    grid-template-columns: 1fr;
    gap: 1rem;
    margin-top: 2.5rem;
  }
}
</style>
