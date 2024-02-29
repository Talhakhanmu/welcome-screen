<script setup>
import { defineProps } from 'vue'

defineProps({
  time: {
    type: String,
    required: true
  },
  topic: {
    type: String,
    required: true
  },
  details: {
    type: String,
    required: true
  }
})
</script>

<template>
  <div class="cards">
    <div class="cardsText">
      <h2>{{ time }}</h2>
      <h3>{{ topic }}</h3>
      <h4>{{ details }}</h4>
    </div>
  </div>
</template>
<style scoped>
h2 {
  font-weight: 900;
  font-size: 28px;
  line-height: 30px;
  color: rgb(252, 63, 63);
}
h3 {
  font-weight: 900;
  font-size: 28px;
  line-height: 30px;
  color: rgb(251, 167, 167);
}
h4 {
  font-size: 28px;
  font-weight: 500;
  line-height: 30px;
  color: rgb(251, 167, 167);
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
</style>
