<script setup>
import { useAnswers } from '@/stores/results'
import { storeToRefs } from 'pinia'
import { computed } from 'vue'
import { personalityTypes } from '@/PersonalityTypes'

const answersSet = useAnswers()
const { traitsCount } = storeToRefs(answersSet)

const personality = computed(() => {
  const t = traitsCount.value
  return [
    t.I >= t.E ? 'I' : 'E',
    t.S >= t.N ? 'S' : 'N',
    t.T >= t.F ? 'T' : 'F',
    t.J >= t.P ? 'J' : 'P',
  ].join('')
})

const personaliytType = personalityTypes.find((type) => type.type === personality.value)
console.log(personaliytType)

const traitPairs = [
  ['I', 'E'],
  ['S', 'N'],
  ['T', 'F'],
  ['J', 'P'],
]

const traitPercents = computed(() =>
  traitPairs.map(([left, right]) => {
    const t = traitsCount.value
    const leftVal = t[left] || 0
    const rightVal = t[right] || 0
    const total = leftVal + rightVal

    return {
      left,
      right,
      leftPercent: total ? Math.round((leftVal / total) * 100) : 0,
      rightPercent: total ? Math.round((rightVal / total) * 100) : 0,
    }
  }),
)
</script>

<template>
  <div class="flex flex-col items-center justify-center h-[50vh] text-black">
    <h1 class="md:text-5xl text-3xl font-bold mb-12 text-[#FFAC8C]">Personality Type</h1>
    <div v-for="pair in traitPercents" :key="pair.left + pair.right" class="w-full max-w-xl mb-6">
      <div class="flex justify-between text-sm mb-1 font-medium text-gray-700">
        <span :class="pair.leftPercent > pair.rightPercent ? 'text-violet-700' : ''"
          >{{ pair.left }} ({{ pair.leftPercent }}%)</span
        >
        <span :class="pair.rightPercent > pair.leftPercent ? 'text-violet-700' : ''"
          >{{ pair.right }} ({{ pair.rightPercent }}%)</span
        >
      </div>
      <div
        class="w-full md:h-4 h-2 bg-gray-200 rounded-full overflow-hidden flex"
        v-if="pair.leftPercent >= pair.rightPercent"
      >
        <div
          class="h-full bg-[#ffdd33] transition-all duration-500"
          :style="{ width: pair.leftPercent + '%' }"
        ></div>
      </div>
      <div class="w-full md:h-4 h-2 bg-[#ffdd33] rounded-full overflow-hidden flex" v-else>
        <div
          class="h-full bg-gray-200 transition-all duration-500"
          :style="{ width: pair.leftPercent + '%' }"
        ></div>
      </div>
    </div>
    <div class="md:text-5xl text-4xl font-extrabold text-[#9cc9df] my-4 border-b-3 border-dotted">
      {{ personality }}
    </div>
    <p>{{ personaliytType.nickname }}</p>
    <p class="my-3 text-center">You are {{ personaliytType.description }}</p>
    <span class="font-medium">Fun Fact: </span>
    <p class="text-sm text-center"> {{ personaliytType.funFact }}</p>
  </div>
</template>
