<template>
  <div>
    <button @click="loadPerformance()">정보가져오기</button><br />
    {{ data }}

    <div>
      아이디:<input type="text" id="id" /><br />
      이름:<input type="text" id="name" /><br />
      비밀번호:<input type="password" id="passwd" /><br />
      나이:<input type="text" id="age" /><br />
      기타 정보:<input type="text" id="ref_val1" /><br />
      <button @click="createInfo()">정보 저장하기</button>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
const data = ref('')
async function loadPerformance() {
  const res = await fetch('http://localhost:3000/api/performance/list')
  const jsonData = await res.json()
  data.value = jsonData
}

async function createInfo() {
  let body = {
    id: document.querySelector('#id').value,
    name: document.querySelector('#name').value,
    passwd: document.querySelector('#passwd').value,
    age: document.querySelector('#age').value,
    ref_val1: document.querySelector('#ref_val1').value
  }

  const res = await fetch('http://localhost:3000/api/performance/create', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json; charset=utf-8',
      // 'Content-Type': 'application/x-www-form-urlencoded',
      body: JSON.stringify(body)
    }
  })
  const jsonData = await res.json()
  data.value = jsonData
}
</script>

<style lang="scss" scoped></style>
