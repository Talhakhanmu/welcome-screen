<script setup>
import { defineProps } from 'vue'
import { computed } from 'vue'

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
const highlightBoolean = computed(() => props.highlight === 'TRUE')

function calculateDaysLeft(targetDate) {
  const [day, month, year] = targetDate.split('.')
  const target = new Date(year, month - 1, day)
  const differenceMs = target - new Date()
  const daysLeft = Math.ceil(differenceMs / (1000 * 60 * 60 * 24))

  return daysLeft
}
const daysLeft = calculateDaysLeft(props.date)
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
  color: rgb(0, 0, 0);
  text-shadow: 0 0 10px rgba(153, 153, 153, 0.8);
}
h3 {
  font-weight: 900;
  font-size: 28px;
  line-height: 30px;
  color: rgb(255, 255, 255);
}
h4 {
  font-size: 28px;
  font-weight: 500;
  line-height: 30px;
  color: rgb(255, 255, 255);
}
.cards {
  width: 960px;
  height: 182px;
  background-color: #0f05a0;
  display: flex;
  margin: 30px;
}
.cardsText {
  width: 755px;
  padding-top: 37px;
  padding-left: 40px;
}
.highlight {
  width: 960px;
  height: 182px;
  background-color: #d10000;
  display: flex;
  margin: 30px;
}
</style>
