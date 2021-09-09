<template>
  <div class="wrapper">
      <div class="cards-container">
        <div v-for="card in cards"
          :class="{card:true, isflipped: card.isFlipped, isSolved: card.isSolved}"
          :key="card.id"
          @click="flipCard(card, $event)"
          >
          <transition name="flip" mode="out-in">
            <div class="cardface" v-if="card.isFlipped" key="front">
              {{ card.picture }}
            </div>
            <div v-else key="back">
              <img src="cardback-small.webp" class="cardback" alt="">
            </div>
          </transition>


        </div>
      </div>
  </div>
</template>

<script>
import {getCards, cardFlipper} from './cards'

export default {
  name: 'TheCardsgameApp',
  props: {
  },
  setup(props) {
    console.log(props)
    let cards = getCards(40);
    return {cards, flipCard: cardFlipper()}
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
* {
  --main-size: 11vw;
}

  .wrapper {
    display: flex;
    justify-content: center;
  }

.cards-container {
  display: grid;
  grid-template-columns: repeat(8, 1fr) ;
  grid-gap: 1vw;
}

.card, .cardback {
  cursor: pointer;
  user-select: none;
  max-width: var(--main-size);
  max-height: var(--main-size);
  font-size: calc(var(--main-size) / 2);
  border-radius: 1vw;
  transform-origin: 50% 50%;
}

.card {
  /* border: 1px solid rgb(68, 68, 68); */
  box-shadow: 12px 10px 8px 4px rgb(194, 194, 194);
}

.cardback {
  margin: auto;
  display: block;
}
.isSolved {
  opacity: .2;
}

</style>
