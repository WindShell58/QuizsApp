<script setup>

import q from '../data/quizes.json'
import {ref,watch} from 'vue'
import Card from '../component/Card.vue'

const quizes = ref(q)
const search = ref('')

// watch almost = listen
watch(search, ()=>{
  // run when search contents changes
  // console.log('you serched: ', search.value)
  // 下面的code直接改动了quizes的内容
  quizes.value = q.filter(quiz => quiz.name.toLowerCase().includes(search.value.toLowerCase()))


})

</script>



<template>
  <div class="container">
    <header>
      <h1>Quizes</h1>
      <input v-model.trim="search" type="text" placeholder="Search...">
    </header>
    <div class="options-container">
      <Card @click="" v-for="quiz in quizes" :key="quiz.id" :quiz="quiz"/>

    </div>
  </div>
</template>


<style scoped>

.container {
  max-width: 1000px;
  margin: 0 auto;
}

header{
  margin-bottom: 10px;
  margin-top: 30px;
  display: flex;
  align-items: center;
}

header h1 {
  font-weight: bold;
  margin-right: 30px;
}

header input {
  border: none;
  padding: 10px;
  border-radius: 5px;
  background-color: rgba(0, 0, 0, 0.1);
}


.options-container {
  display: flex;
  flex-wrap: wrap;
  margin-top: 20px;
}


</style>