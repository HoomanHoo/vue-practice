<script setup>
// import { ref, createApp } from 'vue'

import { ref } from 'vue'
import testVue2 from './vueTest2.vue'
const results = ref('')

async function loadCitiesList() {
  const res = await fetch('http://localhost:3000/api/cities')
  const jsonData = await res.json()
  results.value = jsonData
}
</script>

<template>
  <div id="cityList">
    <button @click="loadCitiesList()">도시 리스트</button>
    <li v-for="result in results">{{ result.name }} / {{ result.location }}</li>
    <br />
  </div>
  <testVue2 />
</template>

<style scoped>
button {
  font-weight: bold;
}
</style>
