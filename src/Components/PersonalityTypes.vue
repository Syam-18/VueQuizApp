<script setup>
import { computed, ref } from 'vue'
import { personalityTypes } from '@/PersonalityTypes'


const searchInput = ref('')
const filteredTypes = computed(() => {
  return personalityTypes.filter(
    (type) => type.type.toLowerCase().includes(searchInput.value.toLowerCase()),
    // || type.nickname.toLowerCase().includes(searchInput.value.toLowerCase()) ||
    // type.description.toLowerCase().includes(searchInput.value.toLowerCase())
  )
})
</script>
<template>
  <div class="text-black w-[50vw]">
    <input
      type="search"
      placeholder="Search Personality Types"
      class="w-[30%] mb-4 p-2 rounded bg-black text-white focus:outline-none"
      v-model="searchInput"
    />
    <h1 class="text-2xl mb-4 font-semibold">Personality Types</h1>
    <table class="w-full">
      <tbody class="w-full">
        <tr>
          <td>Type</td>
          <td>Nickname</td>
          <td>Description</td>
        </tr>
        <tr v-for="data in filteredTypes" :key="data.type">
          <td>{{ data.type }}</td>
          <td>{{ data.nickname }}</td>
          <td>{{ data.description }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
<style scoped>
tr {
  border-bottom: 1px solid black;
}
td {
  padding: 8px;
}
tbody > tr:first-child {
  font-size: 1.2em;
  font-weight: bold;
}
tr > td {
  border: 1px solid black;
  font-size: 1.2rem;
}
tr > td:first-child {
  width: 15%;
  text-align: center;
}
tr > td:nth-child(2) {
  width: 25%;
}
tr > td:nth-child(3) {
  width: 60%;
}
</style>
