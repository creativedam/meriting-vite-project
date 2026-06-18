<script setup>
import { onBeforeUnmount, onMounted, ref } from "vue";
import doc2 from "../assets/docs2.png";
import AppNav from "./AppNav.vue";
import Icon from "./Icon.vue";

const props = defineProps({
  animated: {
    type: Boolean,
    default: false,
  },
});

const audienceWords = ["customer", "stakeholders", "environment"];
const professionWords = ["profession.", "care.", "service."];
const audienceText = ref(props.animated ? "" : audienceWords[0]);
const professionText = ref(props.animated ? "" : professionWords[0]);
const timers = [];

function startTypingLoop(words, output, startDelay = 250) {
  let wordIndex = 0;
  let isDeleting = false;

  function typeNextLetter() {
    const word = words[wordIndex];

    if (!isDeleting && output.value.length < word.length) {
      output.value = word.slice(0, output.value.length + 1);
      timers.push(window.setTimeout(typeNextLetter, 90));
      return;
    }

    if (!isDeleting) {
      isDeleting = true;
      timers.push(window.setTimeout(typeNextLetter, 1400));
      return;
    }

    if (output.value.length > 0) {
      output.value = output.value.slice(0, -1);
      timers.push(window.setTimeout(typeNextLetter, 45));
      return;
    }

    isDeleting = false;
    wordIndex = (wordIndex + 1) % words.length;
    timers.push(window.setTimeout(typeNextLetter, 220));
  }

  timers.push(window.setTimeout(typeNextLetter, startDelay));
}

onMounted(() => {
  if (props.animated) {
    startTypingLoop(audienceWords, audienceText, 250);
    startTypingLoop(professionWords, professionText, 900);
  }
});

onBeforeUnmount(() => {
  timers.forEach((timer) => window.clearTimeout(timer));
});
</script>

<template>
  <header class="home-header">
    <RouterLink to="/" aria-label="Back to home">
      <Icon name="meriting-logo" class="header-logo" />
    </RouterLink>
    <AppNav />
    <!-- <a class="login-link" href="#login" aria-label="Login">
      <span class="lock-mark" aria-hidden="true"></span>
      Login
    </a> -->
  </header>

  <section class="home-hero" aria-labelledby="home-heading">
    <div class="hero-copy">
      <h1 id="home-heading">
        We shall offer, quality driven products and services through recognition and valuing of our
        <span class="typed-word typed-word--audience" :class="{ 'typed-word--active': animated }">
          {{ audienceText }}
        </span>
        and the health
        <span class="typed-word" :class="{ 'typed-word--active': animated }">
          {{ professionText }}
        </span>
      </h1>
    </div>
    <img :src="doc2" alt="Medical team eye logo" class="hero-mark" />
  </section>

  <p class="home-intro">Book appointment online and monitor your application as it gets processed. Ensure your email and phone number is accurate.</p>
</template>

<style scoped>
.home-header {
  position: relative;
  display: grid;
  grid-template-columns: auto auto;
  align-items: center;
  justify-content: space-between;
  gap: 1rem;
  width: min(1020px, 100%);
  margin: 0 auto;
}

.header-logo {
  width: 150px;
}

.login-link {
  position: absolute;
  top: 0.5rem;
  right: 0;
  display: inline-flex;
  align-items: center;
  gap: 0.4rem;
  padding: 0.45rem 0.8rem;
  border-radius: 6px;
  background: #fbfbfd;
  color: #4b5563;
  font-size: 0.9rem;
  font-weight: 700;
}

.lock-mark {
  width: 0.8rem;
  height: 0.65rem;
  border-radius: 2px;
  background: #6b7280;
}

.lock-mark::before {
  display: block;
  width: 0.45rem;
  height: 0.45rem;
  margin: -0.4rem auto 0;
  border: 2px solid #6b7280;
  border-bottom: 0;
  border-radius: 0.45rem 0.45rem 0 0;
  content: "";
}

.home-hero {
  display: grid;
  grid-template-columns: minmax(0, 1fr) 250px;
  gap: 3rem;
  align-items: center;
  width: min(1020px, 100%);
  margin: 1.75rem auto 0;
  padding-bottom: 2rem;
  border-bottom: 2px solid #61d91b;
  text-align: left;
}

h1 {
  max-width: 690px;
  margin: 0;
  color: #26334a;
  font-size: clamp(2rem, 4vw, 3rem);
  font-weight: 400;
  line-height: 1.12;
}

h1 span {
  color: #0067ff;
}

.typed-word {
  display: inline-block;
  color: #0067ff;
}

.typed-word--active::after {
  display: inline-block;
  width: 0.08em;
  height: 0.95em;
  margin-left: 0.08em;
  background: #61d91b;
  vertical-align: -0.1em;
  animation: caret 0.8s step-end infinite;
  content: "";
}

@keyframes caret {
  50% {
    opacity: 0;
  }
}

.hero-mark {
  width: 250px;
}

.home-intro {
  width: min(920px, 100%);
  margin: 1rem auto 0;
  color: #969eaf;
  font-size: clamp(1rem, 2vw, 1.2rem);
  line-height: 1.45;
  text-align: center;
}

@media (max-width: 760px) {
  .home-header {
    grid-template-columns: 1fr;
    justify-items: start;
  }

  .login-link {
    right: 0;
  }

  .home-hero {
    grid-template-columns: 1fr;
    gap: 1.5rem;
    justify-items: center;
    text-align: center;
  }

  .hero-mark {
    width: min(230px, 70vw);
  }
}
</style>
