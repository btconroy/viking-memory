<template>
 
    <div v-for="card in props.deck" :key="card.id" class="flip-card" @click="flippingCardHandler(card.id)">
        <div class="flip-card-inner" :class="{active: card.flip}">
            <div class="flip-card-front">
                <img src="/cards/card_back.svg" alt="back of card" style="width:100%;height:100%;">
            </div>
            <div class="flip-card-back">
                <img :src="card.image" :alt="card.label" style="width:100%;height:100%;">
            </div>
        </div>
    </div>

</template>

<script setup>

import { ref, defineProps, defineEmits } from 'vue'

const props = defineProps({
    deck: {
        type: Array,
        required: true
    }
})

const emits = defineEmits(['gameOver'])

const deck = ref(props.deck)
const matchedCardList = ref([])
const flippedCards = ref([])


const flippingCardHandler = (id) => {
    const pickedCard = deck.value.find(card => card.id === id)
    
    flippedCards.value = flippedCards.value.filter(e => e.id != pickedCard.id); 

    if(flippedCards.value.length === 0) {
        flippedCards.value.push(pickedCard)
        return pickedCard.flip = true
    } else if(checkMatch(pickedCard.label)) {
        matchedCardList.value.push(pickedCard.label)
        if(matchedCardList.value.length === 8) {
            setTimeout(() => {
                emits('gameOver')
                deck.value.forEach(card => {
                    card.flip = false
                })
                matchedCardList.value = []
                flippedCards.value = []
            }, 300)
            return pickedCard.flip = true
        } else {
            flippedCards.value = []
            return pickedCard.flip = true
        }
        
    } else {
        
        pickedCard.flip = true
        flippedCards.value = []
     setTimeout(() => {
        pickedCard.flip = false
        deck.value.forEach(card => {
                if(keepMatchedCards(card.label)) {
                    card.flip = true
                } else {
                    card.flip = false
                }
        })
        }, 680)   
    }
}

const checkMatch = (cardLabel) => {
   return flippedCards.value.filter(e => e.label === cardLabel).length > 0 ? true : false
}

const keepMatchedCards = (cardLabel) => {
  return  matchedCardList.value.filter(e => e === cardLabel).length > 0 ? true : false
}

</script>

<style scoped>

.flip-card {
  background-color: transparent;
  width: 150px;
  height: 150px;
  perspective: 1000px;
}

.flip-card-inner {
  position: relative;
  width: 100%;
  height: 100%;
  text-align: center;
  transition: transform 0.6s;
  transform-style: preserve-3d;
  box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
}

.active {
  transform: rotateY(180deg);
}

.flip-card-front, .flip-card-back {
  position: absolute;
  width: 100%;
  height: 100%;
  border-radius: 10px;
  -webkit-backface-visibility: hidden;
  backface-visibility: hidden;
}
.flip-card-front img, 
.flip-card-back img{
    object-fit: cover;
    object-position: center;
}

.flip-card-front {
  background-color: #bbb;
}

.flip-card-back {
  background-color: #2980b9;
  transform: rotateY(180deg);
}

@media screen and (max-width: 625px) {
    .flip-card {
        width: 100px;
        height: 100px;
    }
}

</style>