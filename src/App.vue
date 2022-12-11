<template>
  <div class="w-full h-full flex justify-center items-center flex-col">
    <span class="text-3xl">Good luck!</span>
    <div class="bg-red-400 p-3 text-gray-50 float-left w-80 rounded-md m-3">{{ question }}</div>
    <div v-if="showAnswer" class="bg-red-400 p-3 text-gray-50 float-right w-80 rounded-md m-3">{{ answer }}</div>
    <button class="bg-blue-700 text-white p-3 rounded-md" v-if="show" @click="getResponse">Another</button>
    <button class="bg-blue-700 text-white p-3 rounded-md" v-else @click="showMe">Tell Me</button>
  </div>
</template>

<script setup>
import { ref } from 'vue'
const question = ref('')
const answer = ref('')
const show = ref(true)
const showAnswer = ref(false)

const showMe = e => {
  console.log(e)
  if (e.target.innerText === 'Tell Me') {
    show.value = true
    return (showAnswer.value = !showAnswer.value)
  }
}
const getResponse = async () => {
  const response = await fetch('https://v2.jokeapi.dev/joke/christmas').then(res => res.json())
  question.value = response.setup
  answer.value = response.delivery
  show.value = false
  showAnswer.value = false
  console.log(show)
}
getResponse()
</script>
