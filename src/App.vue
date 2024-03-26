<script setup>
// Importing necessary components and functions
import HeaderMain from './components/HeaderMain.vue'
import FooterMain from './components/FooterMain.vue'
import CardsMain from './components/CardsMain.vue'
import { ref, onMounted, onBeforeUnmount } from 'vue' // Importing Vue Composition API functions
import { useHead } from '@unhead/vue' // Importing useHead function for managing document head

// Declaring reactive variables
const timeInterval = ref('') // Variable to hold the time interval for data refresh
const sheet_id = import.meta.env.VITE_GOOGLE_SHEET_ID // Google Sheet ID stored in environment variables
const api_token = import.meta.env.VITE_GOOGLE_API_KEY // Google API token stored in environment variables

let fullData = ref([]) // Variable to hold the fetched data from Google Sheets

// Function to fetch data from Google Sheets
async function fetchData() {
  try {
    // Constructing URL for fetching data
    let url = `https://sheets.googleapis.com/v4/spreadsheets/${sheet_id}/values:batchGet?ranges=A2%3AE100&valueRenderOption=FORMATTED_VALUE&key=${api_token}`
    // Fetching data from the constructed URL
    const response = await fetch(url)
    // Parsing response as JSON
    const data = await response.json()
    // Storing fetched data in fullData variable
    fullData.value = data.valueRanges[0].values
    console.log(fullData.value)
  } catch (err) {
    console.error('Error fetching data:', err)
  }
}

// Initial data fetching when the component is mounted
fetchData()

// Set refresh timer to 30 minutes.
onMounted(() => {
  timeInterval.value = setInterval(
    () => {
      fetchData()
    },
    1000 * 60 * 30
  )
})

// Clearing the time interval when the component is unmounted
onBeforeUnmount(() => {
  clearInterval(timeInterval.value)
})

// Setting document head properties using useHead function
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
  <!-- Header component -->
  <HeaderMain />
  <main>
    <!-- Looping through fetched data and passing it to CardsMain component -->
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
  <!-- Footer component -->
  <FooterMain />
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
