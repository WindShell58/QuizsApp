<script setup>
import Question from "@/component/Question.vue";
import QuizHeader from "@/component/QuizHeader.vue";
import { useRoute } from "vue-router";
import {ref, watch, computed} from 'vue'
import quizes from '../data/quizes.json'
import  Result  from '../component/Result.vue'

const route = useRoute()

const quizId = parseInt(route.params.id)
const quiz = quizes.find(q => q.id === quizId)
const numberOfCorectAnswers = ref(0)
const currentQuestionIndex = ref(0)
const showResults = ref(false)
// const questionStatus = ref(`${currentQuestionIndex.value}/${quiz.questions.length}`)

// watch(currentQuestionIndex.value, () => {
//     questionStatus.value = `${currentQuestionIndex.value}/${quiz.questions.length}`
// })

const questionStatus = computed(() => {
    return `${currentQuestionIndex.value}/${quiz.questions.length}`
})


const barPercentage = computed(() => {
    return `${(currentQuestionIndex.value / quiz.questions.length) * 100}%`
})


const OnOptionSelected = (isCorrect) => {
    if(isCorrect) {
        numberOfCorectAnswers.value ++        
    }

    currentQuestionIndex.value ++

}

</script>

<template>
    {{ quizId }}
    <div>
        <QuizHeader 
        :questionStatus="questionStatus"
        :barPercentage="barPercentage"/>
        <div>
            <Question 
            v-if="currentQuestionIndex < quiz.questions.length"
            :question="quiz.questions[currentQuestionIndex]"
            @selectOption="OnOptionSelected"/>
        </div>
        
        <Result 
        v-if="currentQuestionIndex === quiz.questions.length"
        :numberOfCorectAnswers="numberOfCorectAnswers"
        :totalQuestions="quiz.questions.length"
        />
    </div>
</template>

<style scoped></style>
