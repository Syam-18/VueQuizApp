<script setup>
import { ref } from 'vue'
import IndividualDetails from './IndividualDetails.vue'
const isStarted = ref(false)
const handleClose = () => {
  isStarted.value = false
}
</script>

<template>
  <div class="w-[60vw] flex flex-col items-center justify-center text-center">
    <h1 class="md:text-4xl my-4 font-medium text-2xl">MBTI <br> personality test</h1>
    <p class="text-[#555a6a] md:text-lg text-sm">Get a idea about your personality type under 3mins!</p>
    <button
      class="bg-black text-white rounded px-4 py-2 my-3 cursor-pointer"
      @click="isStarted = !isStarted"
    >
      Start Test
    </button>
  </div>
  <div class="fixed inset-0 flex items-center justify-center bg-opacity-50" v-if="isStarted">
    <IndividualDetails class="z-10" @close-modal="handleClose"/>
  </div>
</template>

<style scoped></style>
