<script setup>
import { defineProps } from 'vue';
import {RouterLink} from 'vue-router';

const {numberOfCorectAnswers, totalQuestions} = defineProps(['numberOfCorectAnswers', 'totalQuestions'])


</script>


<template>
    <div class="results">
        <p>Your Results is </p>
        <h1>{{ numberOfCorectAnswers }} / {{ totalQuestions  }}</h1>
    </div>
    <div class="back-to-home">
        <router-link to="/"> start again</router-link>
    </div>
    
</template>


<style scoped>

.results {
    text-align: center;
    padding: 100px 0;
}

p{
    font-size: 25px;
}

h1{
    font-size: 30px;
}

.back-to-home {
    font-size: 30px;
    margin: 30px;
    text-decoration: none;
    padding: 20px 0;
    text-align: center;
}

</style>