<script setup>
import { ref, onMounted, onUnmounted } from "vue";

const hourRotation = ref(0);
const minuteRotation = ref(0);
const secondRotation = ref(0);
let intervalId = null;

const updateClock = () => {
  const now = new Date();
  const seconds = now.getSeconds();
  const minutes = now.getMinutes();
  const hours = now.getHours() % 12; // 12-hour format

  // Hitung derajat rotasi:
  // Detik: (detik * 6 derajat)
  secondRotation.value = seconds * 6;

  // Menit: (menit * 6 derajat) + (detik * 0.1 derajat) untuk gerakan halus
  minuteRotation.value = minutes * 6 + seconds * 0.1;

  // Jam: (jam * 30 derajat) + (menit * 0.5 derajat) untuk gerakan halus
  hourRotation.value = hours * 30 + minutes * 0.5;
};

onMounted(() => {
  updateClock();
  intervalId = setInterval(updateClock, 1000);
});

onUnmounted(() => {
  clearInterval(intervalId);
});
</script>

<template>
  <div class="clock-body">
    <div class="center-dot"></div>
    <div
      class="hand hour"
      :style="{ transform: 'rotate(' + hourRotation + 'deg)' }"
    ></div>
    <div
      class="hand minute"
      :style="{ transform: 'rotate(' + minuteRotation + 'deg)' }"
    ></div>
    <div
      class="hand second"
      :style="{ transform: 'rotate(' + secondRotation + 'deg)' }"
    ></div>
  </div>
</template>

<style scoped>
.clock-body {
  width: 150px;
  height: 150px;
  border-radius: 50%;
  border: 4px solid rgba(255, 255, 255, 0.4);
  position: relative;
  background-color: rgba(0, 0, 0, 0.2);
  margin: 20px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
}

.center-dot {
  width: 10px;
  height: 10px;
  background-color: white;
  border-radius: 50%;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 10;
}

.hand {
  position: absolute;
  bottom: 50%;
  left: 50%;
  transform-origin: bottom;
  transform: translateX(-50%) rotate(0deg);
  border-radius: 5px;
  background-color: white;
  transition: transform 1s cubic-bezier(0.4, 2.3, 0.6, 1); /* Transisi Jarum Jam */
}

.hour {
  width: 4px;
  height: 35%;
  background-color: #f7f7f7;
  z-index: 7;
  transition: transform 0.5s ease-in-out;
}

.minute {
  width: 3px;
  height: 40%;
  background-color: #cccccc;
  z-index: 8;
  transition: transform 0.5s ease-in-out;
}

.second {
  width: 1px;
  height: 45%;
  background-color: #ff3333;
  z-index: 9;
  transition: transform 0.1s linear;
}
</style>
