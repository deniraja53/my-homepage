<script setup>
import { ref, onMounted, onUnmounted } from "vue";

const currentTime = ref("");
const currentDate = ref("");
const intervalId = ref(null);

const updateTime = () => {
  const now = new Date();
  currentTime.value = now.toLocaleTimeString("id-ID", {
    hour: "2-digit",
    minute: "2-digit",
    second: "2-digit",
    hour12: false,
  });
  currentDate.value = now.toLocaleDateString("id-ID", {
    day: "numeric",
    month: "long",
    year: "numeric",
  });
};

onMounted(() => {
  updateTime();
  intervalId.value = setInterval(updateTime, 1000);
});

onUnmounted(() => {
  clearInterval(intervalId.value);
});
</script>

<template>
  <div class="datetime-container">
    <div class="date">{{ currentDate }}</div>
    <div class="time">{{ currentTime }}</div>
  </div>
</template>

<style scoped>
.datetime-container {
  text-align: right;
  font-family: sans-serif;
}
.date {
  font-size: 0.9em;
  opacity: 0.8;
  margin-bottom: 5px;
}
.time {
  font-size: 2.5em;
  font-weight: bold;
  letter-spacing: 2px;
}
</style>
