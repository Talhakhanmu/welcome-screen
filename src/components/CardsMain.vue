<script setup>
// Importing necessary functions from Vue
import { defineProps } from 'vue'
import { computed } from 'vue'

// Defining props for the component
const props = defineProps({
  time: {
    type: String,
    required: true
  },
  topic: {
    type: String,
    required: true
  },
  date: {
    type: String,
    required: true
  },
  address: {
    type: String,
    required: true
  },
  highlight: {
    type: String,
    required: true
  }
})

// Computing a boolean value based on the 'highlight' prop
const highlightBoolean = computed(() => props.highlight === 'TRUE')

// Function to calculate the number of days left until a target date
function calculateDaysLeft(targetDate) {
  const [day, month, year] = targetDate.split('.')
  const target = new Date(year, month - 1, day)
  const differenceMs = target - new Date()
  const daysLeft = Math.ceil(differenceMs / (1000 * 60 * 60 * 24))

  return daysLeft
}

// Calculating the number of days left based on the 'date' prop
const daysLeft = calculateDaysLeft(props.date)

// Determining the message based on the number of days left
let message = ''
if (daysLeft > 0) {
  message = `${daysLeft} days left`
} else if (daysLeft === 0) {
  message = 'Today'
} else {
  message = ''
}
</script>

<template>
  <!-- Template part of the component -->
  <div v-if="daysLeft >= 0" :class="highlightBoolean ? 'highlight' : 'cards'">
    <div class="cardsText">
      <div class="dateNtime">
        <h2>{{ time }}</h2>
        &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp;
        <h4>{{ date }} &nbsp; &nbsp; &nbsp;{{ message }}</h4>
      </div>
      <h3>{{ topic }}</h3>
      <h4>{{ address }}</h4>
    </div>
  </div>
</template>

<style scoped>
.dateNtime {
  display: flex;
  flex-direction: row;
  width: 100%;
}
h2 {
  font-weight: 900;
  font-size: 28px;
  line-height: 30px;
  color: #eb5e00;
}
h3 {
  margin-top: 10px;
  font-weight: 900;
  font-size: 28px;
  line-height: 30px;
  color: #ffbfab;
}
h4 {
  margin-top: 5px;
  font-size: 28px;
  font-weight: 500;
  line-height: 30px;
  color: #ffbfab;
}
.cards {
  width: 960px;
  height: 182px;
  background-color: #0f05a0;
  display: flex;
  margin: 18px;
}
.cardsText {
  width: 755px;
  padding-top: 37px;
  padding-left: 40px;
}
.highlight {
  width: 960px;
  height: 182px;
  background-color: #df0606;
  display: flex;
  margin: 18px;
}
.highlight h2 {
  color: #000000;
}

.highlight h3 {
  color: white;
}

.highlight h4 {
  color: #ffffff;
}
</style>
