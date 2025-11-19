<script setup>
import { ref } from "vue";
// Path relatif dari components/ ke assets/
import linksData from "../assets/links.json";

const links = ref(linksData);
</script>

<template>
  <div class="link-grid">
    <a
      v-for="link in links"
      :key="link.title"
      :href="link.url"
      target="_blank"
      class="link-box"
    >
      <div class="icon">{{ link.icon }}</div>
      <div class="title">{{ link.title }}</div>
    </a>
  </div>
</template>

<style scoped>
.link-grid {
  display: grid;
  /* Membuat kolom fleksibel, min 100px, maksimal 1fr */
  grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
  gap: 20px;
  max-width: 600px; /* Batasi lebar agar terlihat rapi */
  margin: 0 auto; /* Posisikan grid di tengah secara horizontal */
  padding: 20px;
}

.link-box {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 15px;
  border-radius: 12px;
  /* Latar belakang transparan gelap */
  background-color: rgba(255, 255, 255, 0.1);
  text-decoration: none;
  color: white;
  transition: background-color 0.2s, transform 0.2s;
}

.link-box:hover {
  background-color: rgba(255, 255, 255, 0.2);
  transform: translateY(-3px);
}

.icon {
  font-size: 2.5em;
  margin-bottom: 5px;
}

.title {
  font-size: 0.9em;
  font-weight: 500;
}
</style>
