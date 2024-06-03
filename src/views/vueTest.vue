<script setup>
import { ref } from 'vue'
import testVue2 from './vueTest2.vue' //다른 vue 파일을 import하여 화면을 구성할 수 있다
const results = ref('')

async function loadCitiesList() {
  results.value = ''
  //const res = await fetch('http://192.168.16.1:8081/api/cities') //docker로 올라간 nginx container의 주소
  const res = await fetch('http://localhost:3000/api/cities')
  const jsonData = await res.json()
  results.value = jsonData
}

async function loadAnotherInfos() {
  results.value = ''
  const res = await fetch('http://192.168.16.1:8081/second/greeter/hello') //docker로 올라간 nginx container의 주소
  const jsonData = await res.json()
  console.log(jsonData)
  results.value = jsonData
}
</script>

<template>
  <div id="cityList">
    <button @click="loadAnotherInfos()">다른 정보 불러오기</button>
    <button @click="loadCitiesList()">도시 리스트</button>
    <li v-for="result in results">{{ result.name }} / {{ result.location }}</li>
    <br />
  </div>
  <testVue2 />
  <!--해당 위치에서 import해온 vue를 렌더링한다-->
</template>

<style scoped>
button {
  font-weight: bold;
}
</style>
