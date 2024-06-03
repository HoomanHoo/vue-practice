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

const cityList = ref('') //화면에 동적으로 렌더링핧 데이터를 담을 변수를 초기화한다

async function createCityInfo() {
  const data = {
    //DB에 Insert할 데이터를 JSON 타입 Object로 구성한다
    name: document.querySelector('#name').value,
    location: document.querySelector('#location').value
  }

  const res = await fetch('http://localhost:3000/api/save-city', {
    method: 'POST', //통신 방식은 POST를 이용한다
    headers: {
      'Access-Control-Allow-Headers': '*', // this will allow all CORS requests
      'Access-Control-Allow-Methods': 'POST,GET', // this states the allowed methods
      'Content-Type': 'application/json' //JSON을 HTTP Request Body에 담아 전송하기 위해 Content-Type Header를 application/json으로 선언한다
    },
    body: JSON.stringify(data) //JSON형식 Object를 JSON 문자열로 변환하여 Body에 담는다
  })
  const jsonData = await res.json()
  cityList.value = jsonData // return된 값을 렌더링할 데이터를 담기 위해 선언한 변수에 담는다
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
    <!--받아온 데이터를 반복문을 이용하여 li태그로 렌더링한다-->
    <br /><br /><br />
    <input type="button" @click="updateCityInfo()" value="수정" /><br />
    <li v-for="city in cityList">{{ city.name }} / {{ city.location }}</li>
    <br /><br /><br />
    <input type="button" @click="deleteCityInfo()" value="삭제" /><br />
    <li v-for="city in cityList">{{ city.name }} / {{ city.location }}</li>
  </div>
</template>
