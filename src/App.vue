<template>
  <ul>
    <li v-for="(param,i) in params" :key="i">
      <label>key:
        <input v-model="param.key" type="text">
      </label>
      <label>value:
        <input v-model="param.value" type="text">
      </label>
    </li>
  </ul>
  <div>
    <button @click="addParam">+</button>
  </div>
  <label>接口網址
    <input v-model="webAdress" type="text">
  </label>
  <button @click="postApi">試發街口</button>
</template>

<script setup>
import {ref,reactive} from 'vue'
import axios from 'axios'

const webAdress = ref('')
const params = reactive([{key:'',value:''}])
function addParam() {
  params.push({key:'',value:''})
}
async function postApi() {
  const datas = new FormData()
  params.forEach(param=>{
    datas.append(param.key,param.value)
  })
  const result = await axios.post(webAdress.value,datas)
  console.log(result)
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
