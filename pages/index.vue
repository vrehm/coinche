<template>
  <div class="container mx-auto">
    <!-- <h1 class="text-4xl flex justify-start items-center mt-8 mb-4">
      <span class="mr-4">Card Shuffling in</span>
      <img class="h-8" src="https://vuejs.org/images/logo.png" />
    </h1> -->
    <!-- <div class="main-buttons py-4">
      <button class="button is-primary" @click="shuffleDeck">
        Shuffle <i class="fas fa-random"></i>
        Shuffle <fa icon="random" />
      </button>
    </div> -->

    <div class="flex justify-center py-4">
      <button
        class="bg-green-300 hover:bg-green-400 text-green-800 font-bold py-2 px-4 rounded inline-flex items-center focus:outline-none"
        @click="shuffleDeck"
      >
        <span class="pr-2">Shuffle</span>
        <fa icon="random" />
      </button>
    </div>

    <div class="deck">
      <div
        v-for="card in cards"
        :key="card.id"
        class="relative bg-white card"
        :class="suitColor[card.suit]"
      >
        <span class="card__suit card__suit--top">{{ card.suit }}</span>
        <span class="card__number">{{ card.rank }} </span>
        <span class="card__suit card__suit--bottom">{{ card.suit }}</span>
      </div>
    </div>
  </div>

  <!-- <div class="container mx-auto flex justify-center">
    <fa icon="cog" />
    <fa-layers class="fa-4x">
      <fa icon="circle" />
      <fa icon="check" transform="shrink-6" :style="{ color: 'white' }" />
    </fa-layers>
    <fa-layers full-width class="fa-4x">
      <fa icon="calendar" />
      <fa-layers-text
        transform="shrink-8 down-3"
        value="27"
        class="fa-inverse"
      />
    </fa-layers>

    <p style="font-size: 3rem">
      We <fa icon="heart" /> <fa :icon="fab.faJs" />,
      <fa :icon="['fab', 'node']" /> & <fa :icon="['fab', 'vuejs']" />
    </p>
  </div> -->
</template>

<script>
import Vue from 'vue'
// import { faJs } from '@fortawesome/free-brands-svg-icons'

export default {
  data() {
    return {
      ranks: ['7', '8', '9', '10', 'J', 'Q', 'K', 'A'],
      // ranks: ['A', '2', '3', '4', '5', '6', '7', '8', '9', '10', 'J', 'Q', 'K'],
      suits: ['♥', '♦', '♠', '♣'],
      cards: [],
      suitColor: {
        '♠': 'black',
        '♣': 'black',
        '♦': 'red',
        '♥': 'red'
      }
    }
  },
  // computed: {
  //   fab() {
  //     return {
  //       faJs
  //     }
  //   }
  // },
  created() {
    this.displayInitialDeck()
  },
  methods: {
    displayInitialDeck() {
      let id = 1
      this.cards = []

      for (let s = 0; s < this.suits.length; s++) {
        for (let r = 0; r < this.ranks.length; r++) {
          const card = {
            id,
            rank: this.ranks[r],
            suit: this.suits[s]
          }
          this.cards.push(card)
          id++
        }
      }
    },
    shuffleDeck() {
      for (let i = this.cards.length - 1; i > 0; i--) {
        const randomIndex = Math.floor(Math.random() * i)

        const temp = this.cards[i]
        Vue.set(this.cards, i, this.cards[randomIndex])
        Vue.set(this.cards, randomIndex, temp)
      }
    }
  }
}
</script>
