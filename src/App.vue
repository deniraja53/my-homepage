<script setup>
import DateTime from "./components/DateTime.vue";
import LinkBox from "./components/LinkBox.vue";
import AnalogClock from "./components/AnalogClock.vue"; // --- [ PERUBAHAN DI SINI ] ---
</script>

<template>
  <div class="header-content-right">
    <DateTime />
  </div>

  <div class="header-content-left"><AnalogClock /></div>

  <div class="main-content">
    <h1 class="welcome-text">Halo!</h1>
    <LinkBox />
  </div>
</template>

<style scoped>
/* Ubah nama class lama menjadi header-content-right */
.header-content-right {
  position: absolute;
  top: 30px;
  right: 50px;
  width: 300px;
}

/* Styling untuk Jam Analog (Kiri Atas) */
.header-content-left {
  position: absolute;
  top: 30px;
  left: 50px; /* Jarak dari kiri */
  width: 200px;
}

/* Styling untuk konten utama (agar Link Box di tengah layar) */
.main-content {
  text-align: center;

  /* Flexbox untuk pusat vertikal/horizontal */
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
}

/* Styling untuk teks sambutan */
.welcome-text {
  color: white;
  margin-bottom: 50px;
  font-size: 3em;
  font-weight: bold;
}
</style>
