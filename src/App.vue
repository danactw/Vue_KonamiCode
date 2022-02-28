<script setup>
import { ref, computed, watch } from 'vue'

const keyCodeArray = ref([])
const secretCode = ['Up', 'Up', 'Down', 'Down', 'Left', 'Right', 'Left', 'Right', 'B', 'A', 'Ent']
const arrayStart = computed(()=> keyCodeArray.value.length-11)
const arrayEnd = computed(()=> keyCodeArray.value.length)
const keyCodeDisplay = computed(()=> arrayEnd.value < 11 ? keyCodeArray.value : keyCodeArray.value.slice(arrayStart.value, arrayEnd.value))

const getKey = (e) => {
  if(e.key.includes('Arrow')) {
    keyCodeArray.value.push(e.key.slice(5))
  } else if (e.key === 'Enter') {
    keyCodeArray.value.push('Ent')
  } else if (e.key === 'Meta') {
    keyCodeArray.value.push('Cmd')
  } else if (e.key === 'Control') {
    keyCodeArray.value.push('Ctrl')
  } else {
    keyCodeArray.value.push(e.key.toUpperCase())
  }
}

watch(() => keyCodeDisplay.value, function(val) {
  if (secretCode.join('') === val.join('')) {
    keyCodeArray.value = ['H','','E','','L','','L','','O','','!']
  }
})

</script>

<template>
  <div class="container">
    <input type="text" class="shadow" @keydown="getKey">
    <h1 id="title">KONAMI CODE</h1>
    <span class="instruction">請先用滑鼠點擊畫面任一處，並依照下列順序輸入</span>
    <div class="Konami_code">
      <i class="fa fa-arrow-up fa-2x"></i>
      <i class="fa fa-arrow-up fa-2x"></i>
      <i class="fa fa-arrow-down fa-2x"></i>
      <i class="fa fa-arrow-down fa-2x"></i>
      <i class="fa fa-arrow-left fa-2x"></i>
      <i class="fa fa-arrow-right fa-2x"></i>
      <i class="fa fa-arrow-left fa-2x"></i>
      <i class="fa fa-arrow-right fa-2x"></i>
      <span class="hint">B</span>
      <span class="hint">A</span>
      <span class="hint">Ent</span>
    </div>
    <div class="showList">
      <div class="keyItem" v-for="keyItem in keyCodeDisplay" :key="keyItem+ Math.random()"> {{ keyItem }} </div>
    </div>
  </div>
</template>

<style>
  i{
    margin: 20px;
  }

  h1{
    width: 400px;
    font-size: 40px;
    font-weight: 900;
    color: white;
    margin: 20px auto;
    padding: 10px;
    text-align: center;
    background-color: #fa0;
    border-radius: 5px;
  }

  .instruction{
    display: block;
    font-size: 20px;
    margin: auto;
    padding: 10px;
    text-align: center;
  }

  .Konami_code{
    width: 1100px;
    margin: auto;
    text-align: center;
  }

  .hint{
    font-size: 30px;
    font-weight: 900;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    margin: 20px;
  }

  .shadow {
    position: absolute;
    width: 100%;
    height: 100vh;
    opacity: 0;
  }

  .showList {
    display: flex;
    justify-content: center;
    margin-top: 80px;
  }

  .keyItem {
    width: 100px;
    height: 70px;
    margin: 10px;
    border: 2px solid black;
    font-size: 30px;
    font-weight: 900;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    text-align: center;
    padding-top: 25px;
  }
</style>
