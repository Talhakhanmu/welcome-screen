<script>
export default {
  // Method to get the current date

  methods: {
    currentDate() {
      const current = new Date()
      const date = `${current.getDate()}.${current.getMonth() + 1}.${current.getFullYear()}`
      return date
    }
  }
}
</script>

<template>
  <header>
    <h3>Welcome to Opportunity</h3>
    <h2>{{ currentDate() }}</h2>
  </header>
</template>

<style scoped>
h2 {
  width: 335px;
  height: 75px;
  top: 165px;
  left: 60px;
  font-family: Inter;
  font-size: 62px;
  font-weight: 500;
  line-height: 75px;
  letter-spacing: 0em;
  text-align: left;
  color: #9aa7b1;
  margin-left: 50px;
}

h3 {
  width: 764px;
  height: 75px;
  font-family: inter;
  font-size: 62px;
  font-weight: 1700px;
  line-height: 75px;
  letter-spacing: 0em;
  text-align: left;
  color: #323d4a;
  padding-left: 50px;
  padding-top: 50px;
}
header {
  width: 1080px;
  background-color: #e8eff4;
  padding-bottom: 20px;
}
</style>
