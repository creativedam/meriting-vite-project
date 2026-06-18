<template>
  <section class="opening-hours" aria-labelledby="hours-heading">
    <h2 id="hours-heading">Hours</h2>
    <dl class="hours-list">
      <div class="hours-row">
        <dt>Monday</dt>
        <dd>8 am-7 pm</dd>
      </div>
      <div class="hours-row">
        <dt>Tuesday</dt>
        <dd>8 am-7 pm</dd>
      </div>
      <div class="hours-row">
        <dt>Wednesday</dt>
        <dd>8 am-7 pm</dd>
      </div>
      <div class="hours-row">
        <dt>Thursday</dt>
        <dd>8 am-7 pm</dd>
      </div>
      <div class="hours-row">
        <dt>Friday</dt>
        <dd>8 am-7 pm</dd>
      </div>
      <div class="hours-row">
        <dt>Saturday</dt>
        <dd>8 am-6:30 pm</dd>
      </div>
      <div class="hours-row">
        <dt>Sunday</dt>
        <dd>Closed</dd>
      </div>
    </dl>
  </section>
</template>

<style scoped>
.opening-hours {
  display: grid;
  gap: 0.75rem;
}

h2 {
  margin: 0;
  color: #14532d;
  font-size: 1.25rem;
}

.hours-list {
  display: grid;
  gap: 0.4rem;
  margin: 0;
}

.hours-row {
  display: grid;
  grid-template-columns: minmax(7rem, 1fr) auto;
  gap: 1rem;
  align-items: baseline;
}

dt {
  color: #17324d;
  font-weight: 700;
  text-align: left;
}

dd {
  margin: 0;
  color: #4b5563;
  text-align: right;
}
</style>
