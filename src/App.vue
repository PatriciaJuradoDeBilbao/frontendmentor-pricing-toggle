<script setup lang="ts">
import CardComponent from './components/card/Card.vue'
import Data from './data/data.json'
import PriceType from './components/type/PriceType.vue'
import { ref } from 'vue'

const priceType = ref('monthly')

const cardValue = (checked: boolean) => {
  priceType.value = checked === true ? 'monthly' : 'yearly'
}
</script>

<template>
  <div class="wrapper">
    <header class="header">
      <h1>Our Pricing</h1>
      <price-type left-label="Anually" right-label="Montlhy" @input="cardValue" />
    </header>

    <div class="cards">
      <card-component
        v-for="card in Data"
        :key="card.type"
        button-name="LEARN MORE"
        :type="card.type"
        :monthly="card.monthly"
        :yearly="card.yearly"
        :characteristics="card.characteristics"
        :action="card.action"
        :price-type="priceType"
      />
    </div>
  </div>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,700;1,700&display=swap');

h1 {
  color: #6d708d;
  margin-bottom: 12px;
}

.header {
  margin-bottom: 48px;
}

.wrapper {
  font-family: 'Montserrat', sans-serif;
  height: 100%;
  width: 100%;
  display: flex;
  flex-direction: column;
  background-color: #f6f6fe;
  padding: 56px 16px 36px 16px;
  align-items: center;
  background-image: url(./assets//images/bg-top.svg), url(./assets//images/bg-bottom.svg);
  background-position:
    left 185px top -40px,
    left -750px top;
  background-size: contain;
  background-repeat: no-repeat;
}

@media (min-width: 768px) {
  .wrapper {
    height: 100vh;
    background-position:
      right top,
      left bottom;
    background-size: 30%;
  }
}

@media (min-width: 768px) {
  .cards {
    display: flex;
    width: 100%;
    max-height: 1000px;
    padding: 56px 120px 60px 120px;
    align-items: center;
  }
}
</style>