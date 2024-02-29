<script setup>
import HeaderMain from './components/HeaderMain.vue'
import FooterMain from './components/FooterMain.vue'
import CardsMain from './components/CardsMain.vue'
import { ref, onMounted } from 'vue'

const sheet_id = import.meta.env.VITE_GOOGLE_SHEET_ID
const api_token = import.meta.env.VITE_GOOGLE_API_KEY

let fullData = ref([])
async function fetchData() {
  try {
    let url = `https://sheets.googleapis.com/v4/spreadsheets/${sheet_id}/values:batchGet?ranges=A2%3AE100&valueRenderOption=FORMATTED_VALUE&key=${api_token}`
    const response = await fetch(url)
    const data = await response.json()
    fullData.value = data.valueRanges[0].values
  } catch (err) {
    console.error('Error fetching data:', err)
  }
}
fetchData()
</script>

<template>
  <header>
    <HeaderMain />
  </header>
  <main>
    <CardsMain
      v-for="(event, index) in fullData"
      :key="index"
      :time="event[0]"
      :topic="event[2]"
      :details="event[3]"
    />
  </main>
  <footer>
    <FooterMain />
  </footer>
</template>
<style scoped>
main {
  background-color: #e8eff4;
  width: 1080px;
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
