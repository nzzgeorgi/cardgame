<template>
  <div class="wrapper">
      <div class="cards-container">
        <div v-for="card in cards"
          :class="{card:true, isflipped: card.isFlipped, isSolved: card.isSolved}"
          :key="card.id"
          @click="flipCard(card, this)"
          @success="playSoundSuccess"
          >
            <div class="cardface" v-if="card.isFlipped" key="front">
              {{ card.picture }}
            </div>
            <div v-else key="back">
              <img src="@/assets/cardback-small.webp" class="cardback" alt="">
            </div>
        </div>
      </div>
  </div>
</template>

<script>
/* eslint-disable */
import {getCards, cardFlipper} from './cards'

export default {
  name: 'TheCardsgameApp',
  props: {
  },
  emits : ['success'],

  setup(props, { emit }) {
    let cards = getCards(40);
    var audio = new Audio(require('@/assets/success-sound-effect.mp3'))
    audio.volume = 0.3;

    function playSoundSuccess() {
      audio.currentTime=0
      audio.play()
    }

    return {cards, flipCard: cardFlipper(), playSoundSuccess}
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
  box-shadow: 4px 4px 8px 2px rgb(194, 194, 194);
}

.cardback {
  margin: auto;
  display: block;
}
.isSolved {
  opacity: .2;
}

</style>
