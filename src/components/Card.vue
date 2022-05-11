<template>
    <!-- The default setting for the card is that it is not flipped over and not facing up.
    The 'not-flipped' class will have nothing but a background and a placeholder icon
    displayed via CSS as long as the card.flipped is false. -->
  <div @click="flipCard()" :class="[card.flipped ? '' : 'not-flipped', 'card']">
    <header>
      <h3>{{ card.name }}</h3>
    </header>
    <body>
      <div class="unflipped">໒(・ᴥ・)७</div>
      <img v-bind:src="card.image" />
    </body>
    <footer>
      <div>{{ card.rarity }}</div>
    </footer>
  </div>
</template>

<script>
export default {
  name: "Card",
  props: {
    name: {
      type: String,
      default: "",
    },
    image: {
    type: String,
      default: "",
    },
    card: {
      type: Object,
      default: {},
    },
  },
  methods: {
      //This is the method that will go up two levels from Cards.vue to App.vue.
    async flipCard(id) {
      this.$emit("flip-card");
    },
  },
};
</script>

<style scoped>
header {
  width: 100%;
  border-bottom: white 1px solid;
}
footer {
  color: goldenrod;
}
.unflipped {
  display: none;
}
.card {
  width: 150px;
  height: 290px;
  color: rgb(230, 230, 230);
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
  border: solid 2px black;
  background-image: linear-gradient(rgb(163, 163, 248), rgb(62, 69, 170));
}

img {
  width: 90px;
  height: 90px;
  border-radius: 100%;
  border: 2px rgb(255, 255, 255) solid;
}

/* Everything here is to make sure nothing is displaying
(with the exception of the placeholder emoticon) when the card 
is not "flipped" yet. */
.not-flipped img {
  display: none;
}
.not-flipped header {
  display: none;
}
.not-flipped footer {
  display: none;
}
.not-flipped .unflipped {
  display: contents;
}
</style>