<script setup>
import HeaderMain from './components/HeaderMain.vue'
import FooterMain from './components/FooterMain.vue'
import CardsMain from './components/CardsMain.vue'
</script>
<template>
  <header>
    <HeaderMain />
  </header>
  <main>
    <CardsMain />
    <CardsMain />
    <CardsMain />
  </main>
  <footer>
    <FooterMain />
  </footer>
</template>

<style scoped>
main {
  width: 1080px;
  background-color: #e8eff4;
}
</style>
