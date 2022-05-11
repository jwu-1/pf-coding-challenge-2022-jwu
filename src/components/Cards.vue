<template>
  <div id="cards">
    <div class="row">
      <div :key="card.id" v-for="card in cards">
          <!-- The $emit will transfer from the Card.vue to the main App.vue -->
        <Card @flip-card="$emit('flip-card',card.id)" :card= "card"/>
      </div>
    </div>
    <div class="row">
      <div :key="card.id" v-for="card in secondCards">
        <Card @flip-card="$emit('flip-card',card.id)" :card= "card"/>
      </div>
    </div>
  </div>
</template>

<script>
import Card from "./Card.vue";
export default {
  name: "Cards",
  props: {
    cards: {
      type: Array,
      default: [],
    },
    secondCards: {
      type: Array,
      default: [],
    },
  },
  components: {
    Card,
  },
};
</script>

<style>
#cards {
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
.row {
  display: flex;
}
</style>