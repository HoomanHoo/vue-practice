<script setup>
import { ref, createApp } from 'vue'

const app = createApp({
  data() {
    return {
      count2: 0
    }
  }
})
app.mount('#app2')

const cityList = ref('')

async function createCityInfo() {
  const data = {
    name: document.querySelector('#name').value,
    location: document.querySelector('#location').value
  }

  const res = await fetch('http://localhost:3000/api/save-city', {
    method: 'POST',
    headers: {
      'Access-Control-Allow-Headers': '*', // this will allow all CORS requests
      'Access-Control-Allow-Methods': 'POST,GET', // this states the allowed methods
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(data)
  })
  const jsonData = await res.json()
  cityList.value = jsonData
}

async function updateCityInfo() {
  //도시정보 수정
  const data = {
    name: document.querySelector('#name').value,
    location: document.querySelector('#location').value
  }

  const res = await fetch('http://localhost:3000/api/update-city', {
    method: 'PUT',
    headers: {
      'Access-Control-Allow-Headers': '*', // this will allow all CORS requests
      'Access-Control-Allow-Methods': 'PUT,GET', // this states the allowed methods
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(data)
  })
  const jsonData = await res.json()
  cityList.value = jsonData
}

async function deleteCityInfo() {
  //도시정보 삭제
  const data = {
    name: document.querySelector('#name').value,
    location: document.querySelector('#location').value
  }

  const res = await fetch('http://localhost:3000/api/remove-city', {
    method: 'DELETE',
    headers: {
      'Access-Control-Allow-Headers': '*', // this will allow all CORS requests
      'Access-Control-Allow-Methods': 'DELETE,GET', // this states the allowed methods
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(data)
  })
  const jsonData = await res.json()
  cityList.value = jsonData
}
</script>

<template>
  <div id="app2">
    도시 이름: <input type="text" id="name" /><br />
    도시 좌표: <input type="text" id="location" /><br />
    <input type="button" @click="createCityInfo()" value="저장" /><br />
    <li v-for="city in cityList">{{ city.name }} / {{ city.location }}</li>
    <br /><br /><br />
    <input type="button" @click="updateCityInfo()" value="수정" /><br />
    <li v-for="city in cityList">{{ city.name }} / {{ city.location }}</li>
    <br /><br /><br />
    <input type="button" @click="deleteCityInfo()" value="삭제" /><br />
    <li v-for="city in cityList">{{ city.name }} / {{ city.location }}</li>
  </div>
</template>
