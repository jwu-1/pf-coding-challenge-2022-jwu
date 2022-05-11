<template>
  <Title/>
  <!-- 
  flipCard() is a function that is activated moving from the components of
  Card->Cards->Here 
  -->
  <Cards @flip-card = "flipCard" :cards = "cards" :secondCards = "secondCards"/>
</template>

<script>
import Title from "./components/Title.vue";
import Cards from "./components/Cards.vue";

export default {
  name: "App",
  components: {
    Title,
    Cards,
  },
  data() {
    return {
      //This was a quick way to separate the 10 cards into two different rows
      //by creating two different arrays.
      cards: [],
      secondCards:[],
    };
  },
  methods:{
    //This is the method used from the Card component which is
    //two levels down. The cards in the arrays on line 24 and 25 will
    //have objects with a boolean on whether or not the card is flipped.
    flipCard(id){
      this.cards.forEach(card=>{
        if (card.id === id){
          if(card.flipped){
            card.flipped = false
          }else{
            card.flipped = true
          }
        }
      })
      this.secondCards.forEach(card=>{
        if (card.id === id){
          if(card.flipped){
            card.flipped = false
          }else{
            card.flipped = true
          }
        }
      })
    }
  },
  async created() {
    //The names in these two arrays will be selected at random using
    //Math.random() method to make sure that each card is unique.
    const dogNames = [
      "Minnie",
      "Rusty",
      "Sam",
      "Guinness",
      "George",
      "Mac",
      "Sally",
      "Roxie",
      "Mia",
      "Rocky",
      "Koda",
      "Athena",
      "Bailey",
      "Whiskey",
      "Buddy",
      "Bo",
      "Chester",
      "Frankie",
      "Simba",
      "Molly",
    ];
    const rarities = [
      "Common",
      "Uncommon",
      "Pretty Rare",
      "Rare",
      "Very Rare",
      "Ultra Rare",
      "Mega Rare",
      "Ultimate Rare",
      "Legendary"
    ]
    //The cards are being made into objects here with the image url being fetched
    //from the url that was given.
    while (this.cards.length < 5) {
      const dogName =dogNames[Math.floor(Math.random() * dogNames.length)]
      const rarity = rarities[Math.floor(Math.random() * rarities.length)]
      const res = await fetch("https://dog.ceo/api/breeds/image/random");
      const data = await res.json();
      const dogImage = data.message;
      this.cards.push({
        name:dogName,
        image:dogImage,
        rarity,
        id: this.cards.length,
        flipped: false
      });
    }
    //The same action of fetching the image and creating a card object applies
    //to the second row of cards.
    while (this.secondCards.length < 5) {
      const dogName =dogNames[Math.floor(Math.random() * dogNames.length)]
      const rarity = rarities[Math.floor(Math.random() * rarities.length)]
      const res = await fetch("https://dog.ceo/api/breeds/image/random");
      const data = await res.json();
      const dogImage = data.message;
      this.secondCards.push({
        name:dogName,
        image:dogImage,
        rarity,
        id: this.secondCards.length+this.cards.length,
        flipped: false
      });
    }
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Exo:wght@500&family=Raleway&display=swap");
#app {
  font-family: "Raleway", Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
