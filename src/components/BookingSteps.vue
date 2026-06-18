<script setup>
import Icon from "./Icon.vue";
</script>

<template>
  <section class="booking-steps" aria-labelledby="booking-heading">
    <h2 id="booking-heading">How To Book</h2>

    <article class="step-row">
      <div class="step-copy">
        <h3>Call or WhatsApp</h3>
        <p>
          Reach out to us by
          <span>phone</span>
          or
          <strong>WhatsApp</strong>
          and our team will help you book your appointment.
        </p>
      </div>
      <div class="step-number" aria-label="Step 1">
        <small>Step</small>
        <strong>01</strong>
      </div>
      <Icon name="cellphone" class="step-icon step-icon--cellphone" />
    </article>

    <article class="step-row step-row--reverse">
      <Icon name="phone-approval-chat" class="step-icon step-icon--phone" />
      <div class="step-number" aria-label="Step 2">
        <small>Step</small>
        <strong>02</strong>
      </div>
      <div class="step-copy">
        <h3>Reservation Notification</h3>
        <p>
          You will receive a receipt of your reservation via
          <span>Email</span>
          , SMS and
          <strong>Whatsapp</strong>
          . Another notification will be sent after reservation has been approved.
        </p>
      </div>
    </article>
  </section>
</template>

<style scoped>
.booking-steps {
  width: min(1000px, 100%);
  margin: 3.5rem auto 0;
}

.booking-steps > h2 {
  margin: 0 0 2rem;
  color: #050505;
  font-size: clamp(1.75rem, 3vw, 2.25rem);
  font-weight: 900;
  text-align: center;
  text-transform: uppercase;
}

.booking-steps > h2::after {
  display: block;
  width: 140px;
  height: 1px;
  margin: 1.5rem auto 0;
  background: #d9dde7;
  content: "";
}

.step-row {
  display: grid;
  grid-template-columns: minmax(0, 1fr) 110px minmax(0, 1fr);
  gap: 2rem;
  align-items: center;
  min-height: 260px;
  padding: 2rem 0;
  border-bottom: 4px dotted #aeb8c8;
}

.step-copy {
  text-align: left;
}

.step-row--reverse .step-copy {
  max-width: 360px;
}

.step-copy h3 {
  margin: 0 0 0.75rem;
  color: #111111;
  font-size: 1rem;
  font-weight: 500;
}

.step-copy p {
  margin: 0;
  color: #344054;
  font-size: 0.85rem;
  line-height: 1.55;
}

.step-copy span {
  color: #0067ff;
  font-weight: 800;
}

.step-copy strong {
  color: #12a60c;
}

.step-number {
  display: grid;
  align-content: start;
  justify-items: center;
  align-self: stretch;
  padding-top: 1rem;
  border-right: 4px dotted #e1e6ef;
  border-left: 4px dotted #e1e6ef;
  text-transform: uppercase;
}

.step-number small {
  color: #9aa3b5;
  font-size: 0.8rem;
  font-weight: 800;
}

.step-number strong {
  color: #050505;
  font-size: 2rem;
  line-height: 1;
}

.step-icon {
  justify-self: center;
  object-fit: contain;
}

.step-icon--cellphone {
  width: 153px;
}

.step-icon--phone {
  width: 150px;
}

@media (max-width: 760px) {
  .step-row,
  .step-row--reverse {
    grid-template-columns: 1fr;
    gap: 1.25rem;
    justify-items: center;
    min-height: auto;
  }

  .step-row--reverse .step-icon {
    order: 3;
  }

  .step-row--reverse .step-number {
    order: 1;
  }

  .step-row--reverse .step-copy {
    order: 2;
  }

  .step-copy,
  .step-row--reverse .step-copy {
    max-width: 520px;
    text-align: center;
  }

  .step-number {
    width: 110px;
    min-height: 100px;
  }
}
</style>
