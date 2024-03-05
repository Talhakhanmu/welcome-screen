<script setup>
import HeaderMain from './components/HeaderMain.vue'
import FooterMain from './components/FooterMain.vue'
import CardsMain from './components/CardsMain.vue'
import { ref, onMounted, onBeforeUnmount } from 'vue'
import { useHead } from '@unhead/vue'

const timeInterval = ref('')
const sheet_id = import.meta.env.VITE_GOOGLE_SHEET_ID
const api_token = import.meta.env.VITE_GOOGLE_API_KEY

let fullData = ref([])

async function fetchData() {
  try {
    let url = `https://sheets.googleapis.com/v4/spreadsheets/${sheet_id}/values:batchGet?ranges=A2%3AE100&valueRenderOption=FORMATTED_VALUE&key=${api_token}`
    const response = await fetch(url)
    const data = await response.json()
    fullData.value = data.valueRanges[0].values
    console.log(fullData.value)
  } catch (err) {
    console.error('Error fetching data:', err)
  }
}
fetchData()
onMounted(() => {
  timeInterval.value = setInterval(
    () => {
      fetchData()
      getData()
    },
    1000 * 60 * 30
  )
})
onBeforeUnmount(() => {
  clearInterval(timeInterval.value)
})

useHead({
  title: 'welcome-screen',
  meta: [
    {
      name: 'description',
      content: 'The welcome screen'
    }
  ]
})
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
      :date="event[1]"
      :topic="event[2]"
      :address="event[3]"
      :highlight="event[4]"
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
