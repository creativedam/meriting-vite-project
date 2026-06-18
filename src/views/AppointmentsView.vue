<script setup>
import { computed, ref } from "vue";
import AppNav from "../components/AppNav.vue";
import Icon from "../components/Icon.vue";

const today = new Date(Date.now());
const activeWeekStart = ref(getMonday(today));
const scheduleHours = buildScheduleHours();

const weekOptions = computed(() => {
  const currentWeekStart = getMonday(today);

  return Array.from({ length: 5 }, (_, index) => {
    const weekStart = addDays(currentWeekStart, index * 7);

    return {
      label: index === 0 ? "Current week" : formatWeekStart(weekStart),
      weekStart,
    };
  });
});

const weekDays = computed(() => {
  return Array.from({ length: 7 }, (_, index) => addDays(activeWeekStart.value, index));
});

const activeWeekLabel = computed(() => {
  const activeOption = weekOptions.value.find((option) => isSameDay(option.weekStart, activeWeekStart.value));
  return activeOption?.label || formatWeekStart(activeWeekStart.value);
});

function addDays(date, days) {
  const nextDate = new Date(date);
  nextDate.setDate(date.getDate() + days);
  return nextDate;
}

function getMonday(date) {
  const monday = new Date(date);
  const day = monday.getDay() || 7;
  monday.setHours(0, 0, 0, 0);
  monday.setDate(monday.getDate() - day + 1);
  return monday;
}

function isSameDay(firstDate, secondDate) {
  return firstDate.getFullYear() === secondDate.getFullYear() && firstDate.getMonth() === secondDate.getMonth() && firstDate.getDate() === secondDate.getDate();
}

function isToday(date) {
  return isSameDay(date, today);
}

function isCurrentSession(date, session) {
  if (!isToday(date)) {
    return false;
  }

  const currentMinutes = today.getHours() * 60 + today.getMinutes();
  return currentMinutes >= session.startMinutes && currentMinutes <= session.endMinutes;
}

function formatDay(date) {
  return new Intl.DateTimeFormat("en", {
    weekday: "short",
    month: "short",
    day: "numeric",
  }).format(date);
}

function formatFullDate(date) {
  return new Intl.DateTimeFormat("en", {
    weekday: "long",
    year: "numeric",
    month: "long",
    day: "numeric",
  }).format(date);
}

function formatWeekStart(date) {
  return new Intl.DateTimeFormat("en", {
    month: "long",
    day: "numeric",
  }).format(date);
}

function formatHour(hour) {
  return `${String(hour).padStart(2, "0")}:00`;
}

function formatMinutes(totalMinutes) {
  const hour = Math.floor(totalMinutes / 60);
  const minutes = totalMinutes % 60;
  return `${String(hour).padStart(2, "0")}:${String(minutes).padStart(2, "0")}`;
}

function isCurrentHour(date, hourBlock) {
  return isToday(date) && today.getHours() === hourBlock.hour;
}

function buildScheduleHours() {
  const hourBlocks = [];

  for (let hour = 7; hour <= 18; hour += 1) {
    if (hour < 8 || hour > 17 || hour === 13) {
      hourBlocks.push({
        id: `${hour}-closed`,
        hour,
        label: formatHour(hour),
        closed: true,
        lunch: hour === 13,
        sessions: [],
      });
      continue;
    }

    hourBlocks.push({
      id: `${hour}-open`,
      hour,
      closed: false,
      sessions: [
        {
          id: `${hour}-first`,
          label: `${formatMinutes(hour * 60)}-${formatMinutes(hour * 60 + 20)}`,
          startMinutes: hour * 60,
          endMinutes: hour * 60 + 20,
        },
        {
          id: `${hour}-second`,
          label: `${formatMinutes(hour * 60 + 30)}-${formatMinutes(hour * 60 + 55)}`,
          startMinutes: hour * 60 + 30,
          endMinutes: hour * 60 + 55,
        },
      ],
    });
  }

  return hourBlocks;
}

function seededSlotValue(date, session) {
  const seed = date.getFullYear() * 10000 + (date.getMonth() + 1) * 100 + date.getDate() + session.startMinutes * 17;
  return Math.abs(Math.sin(seed) * 10000) % 1;
}

function sessionState(date, session) {
  return seededSlotValue(date, session) > 0.62 ? "booked" : "available";
}

function sessionLabel(date, session) {
  if (isCurrentSession(date, session)) {
    return "Current time";
  }

  return sessionState(date, session) === "booked" ? "Booked" : "Available";
}

function hourLabel(hourBlock) {
  return hourBlock.lunch ? "Lunch" : "Closed";
}
</script>

<template>
  <main class="appointments-view">
    <section class="appointments-hero">
      <div class="appointments-topbar">
        <RouterLink to="/" aria-label="Go to home">
          <Icon name="meriting-logo" class="appointments-logo" />
        </RouterLink>
        <h1>Appointments</h1>
        <AppNav />
      </div>
      <p>Choose a week to view available and booked appointment slots.</p>
      <p class="today-date">Today: {{ formatFullDate(today) }}</p>
    </section>

    <section class="week-picker" aria-label="Weeks of the year">
      <button v-for="week in weekOptions" :key="week.weekStart.toISOString()" type="button" :class="{ active: isSameDay(week.weekStart, activeWeekStart) }" @click="activeWeekStart = week.weekStart">
        {{ week.label }}
      </button>
    </section>

    <section class="calendar-card" aria-label="Appointment calendar">
      <div class="calendar-heading">
        <div>
          <h2>Booking schedule for the next 4 weeks</h2>
          <p class="schedule-note">Dr Ntwaagae has a 5-10 minute doctor buffer between sessions.</p>
          <p class="active-week-label">{{ activeWeekLabel }}</p>
        </div>
        <div class="legend" aria-label="Slot legend">
          <span class="legend-item legend-item--available">Available</span>
          <span class="legend-item legend-item--booked">Booked</span>
          <span class="legend-item legend-item--current">Current time</span>
          <span class="legend-item legend-item--closed">Lunch / Closed</span>
        </div>
      </div>

      <div class="calendar-grid">
        <div class="calendar-corner">Time</div>
        <div v-for="day in weekDays" :key="day.toISOString()" class="calendar-day" :class="{ 'calendar-day--today': isToday(day) }">
          {{ formatDay(day) }}
        </div>

        <template v-for="hourBlock in scheduleHours" :key="hourBlock.id">
          <div class="time-label">{{ hourBlock.label }}</div>
          <div
            v-for="day in weekDays"
            :key="`${day.toISOString()}-${hourBlock.id}`"
            class="slot-cell"
            :class="[
              {
                'slot--today': isToday(day),
                'slot-cell--closed': hourBlock.closed,
                'slot--current': isCurrentHour(day, hourBlock),
              },
            ]"
          >
            <span v-if="hourBlock.closed" class="closed-label">{{ hourLabel(hourBlock) }}</span>
            <button v-for="session in hourBlock.sessions" v-else :key="session.id" type="button" class="session-slot" :class="[`session-slot--${sessionState(day, session)}`, { 'session-slot--current': isCurrentSession(day, session) }]">
              <span>{{ session.label }}</span>
              <span>{{ sessionLabel(day, session) }}</span>
            </button>
          </div>
        </template>
      </div>
    </section>
  </main>
</template>

<style scoped>
.appointments-view {
  width: min(1180px, 100%);
  margin: 0 auto;
  padding: 2rem 1.5rem 0;
}

.appointments-hero {
  display: grid;
  gap: 0.5rem;
  padding-bottom: 1.5rem;
  border-bottom: 2px solid #61d91b;
}

.appointments-topbar {
  display: grid;
  grid-template-columns: auto minmax(0, 1fr) auto;
  gap: 1rem;
  align-items: center;
  text-align: left;
}

.appointments-logo {
  width: 128px;
}

h1 {
  margin: 0;
  color: #26334a;
  font-size: clamp(2.25rem, 5vw, 4rem);
  text-align: center;
}

.appointments-hero p {
  margin: 0;
  color: #7b8493;
  font-size: 1.1rem;
}

.appointments-hero .today-date {
  color: #005ee4;
  font-weight: 800;
}

.week-picker {
  display: flex;
  gap: 0.5rem;
  margin: 2rem 0;
  padding-bottom: 0.5rem;
  overflow-x: auto;
}

.week-picker button {
  flex: 0 0 auto;
  border: 1px solid #cbd5e1;
  border-radius: 6px;
  background: #ffffff;
  color: #344054;
  font-weight: 700;
}

.week-picker button.active {
  border-color: #005ee4;
  background: #005ee4;
  color: #ffffff;
}

.calendar-card {
  padding: 1rem;
  border: 1px solid #d7ead9;
  border-radius: 8px;
  background: #ffffff;
  overflow-x: auto;
}

.calendar-heading {
  display: flex;
  justify-content: space-between;
  gap: 1rem;
  align-items: center;
  margin-bottom: 1rem;
  text-align: left;
}

h2 {
  margin: 0;
  color: #14532d;
  font-size: 1.3rem;
}

.schedule-note {
  max-width: 720px;
  margin: 0.4rem 0 0;
  color: #4b5563;
  font-size: 0.92rem;
  line-height: 1.5;
}

.active-week-label {
  margin: 0.55rem 0 0;
  color: #005ee4;
  font-size: 0.95rem;
  font-weight: 600;
}

.legend {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.legend-item {
  padding: 0.35rem 0.55rem;
  border-radius: 4px;
  color: #17324d;
  font-size: 0.8rem;
  font-weight: 600;
}

.legend-item--available {
  background: #c8f7c8;
}

.legend-item--booked {
  background: #ffc9c9;
}

.legend-item--current {
  background: #dbeafe;
  color: #005ee4;
}

.legend-item--closed {
  background: #e5e7eb;
}

.calendar-grid {
  display: grid;
  grid-template-columns: 88px repeat(7, minmax(130px, 1fr));
  gap: 0.4rem;
  min-width: 1040px;
}

.calendar-corner,
.calendar-day,
.time-label {
  display: grid;
  place-items: center;
  min-height: 44px;
  border-radius: 5px;
  background: #f4f7fb;
  color: #344054;
  font-weight: 600;
}

.calendar-day--today {
  border: 2px solid #005ee4;
  background: #dbeafe;
  color: #005ee4;
}

.slot-cell {
  display: grid;
  gap: 0.4rem;
  min-height: 76px;
  padding: 0.5rem;
  border: 1px solid transparent;
  border-radius: 6px;
  color: #17324d;
  text-align: left;
}

.slot-cell--closed {
  place-items: center;
  background: #e5e7eb;
  border-color: #cbd5e1;
  color: #667085;
}

.closed-label {
  font-size: 0.9rem;
}

.slot--today {
  border-color: #60a5fa;
}

.slot--current {
  border: 3px solid #005ee4;
  color: #005ee4;
  box-shadow: inset 0 0 0 1px #005ee4;
}

.session-slot {
  display: grid;
  gap: 0.15rem;
  width: 100%;
  min-height: 34px;
  padding: 0.35rem 0.45rem;
  border: 1px solid transparent;
  border-radius: 5px;
  color: #17324d;
  font: inherit;
  font-size: 0.82rem;
  font-weight: 400;
  line-height: 1.2;
  text-align: left;
}

.session-slot--available {
  background: #c8f7c8;
  border-color: #7ddb7d;
}

.session-slot--booked {
  background: #ffc9c9;
  border-color: #f49999;
}

.session-slot--current {
  border: 2px solid #005ee4;
  color: #005ee4;
}

@media (max-width: 760px) {
  .appointments-topbar {
    grid-template-columns: 1fr;
    justify-items: start;
  }

  .calendar-heading {
    align-items: flex-start;
    flex-direction: column;
  }
}
</style>
