<template>
  <h1>Viking Memory</h1>
  <Timer :min="min" :sec="sec" />
  <MainBoard>
    <CardList :deck="deck" @gameOver="gameEnds" />
  </MainBoard>
  <Modal @play="startGame" :input="talk" :retry="redo" :start="start" />
</template>

<script setup>
  import MainBoard from './components/MainBoard.vue'
  import CardList from './components/CardList.vue'
  import Timer from './components/Timer.vue'
  import Modal from './components/Modal.vue'
  import { ref, reactive, computed } from 'vue'

const min = ref(0)
const sec = ref('00')
const start = ref(false)
const redo = ref(false)
const talk = ref("Let's see how sharp your memory is!")

const deck = ref([
    {
        id: 4,
        label: 'coins',
        image: '/cards/coins-card.svg',
        flip: false
    },
    {
        id: 0,
        label: 'sword',
        image: '/cards/sword-card.svg',
        flip: false
    },
    {
        id: 1,
        label: 'ship',
        image: '/cards/ship-card.svg',
        flip: false
    },
    {   id: 2,
        label: 'sheild',
        image: '/cards/sheild-card.svg',
        flip: false
    },
    {
        id: 22,
        label: 'ship',
        image: '/cards/ship-card.svg',
        flip: false
    },
    {   id: 29,
        label: 'sheild',
        image: '/cards/sheild-card.svg',
        flip: false
    },
    {
        id: 3,
        label: 'hammer',
        image: '/cards/hammer-card.svg',
        flip: false
    },
    {
        id: 8,
        label: 'sword',
        image: '/cards/sword-card.svg',
        flip: false
    },
    {
        id: 11,
        label: 'hammer',
        image: '/cards/hammer-card.svg',
        flip: false
    },
    {
        id: 46,
        label: 'coins',
        image: '/cards/coins-card.svg',
        flip: false
    },
    {
        id: 5,
        label: 'helmet',
        image: '/cards/card_helmet.svg',
        flip: false
    },
    {
        id: 73,
        label: 'ale horn',
        image: '/cards/ale-horn-card.svg',
        flip: false
    },
    {
        id: 6,
        label: 'ax',
        image: '/cards/ax-card.svg',
        flip: false
    },
    {
        id: 51,
        label: 'helmet',
        image: '/cards/card_helmet.svg',
        flip: false
    },
    {
        id: 7,
        label: 'ale horn',
        image: '/cards/ale-horn-card.svg',
        flip: false
    },
    {
        id: 62,
        label: 'ax',
        image: '/cards/ax-card.svg',
        flip: false
    }
])

const shuffle = () => {
    let currentIndex = deck.value.length,  randomIndex
  while (currentIndex > 0) {

    randomIndex = Math.floor(Math.random() * currentIndex)
    currentIndex--

    [deck.value[currentIndex], deck.value[randomIndex]] = [
    deck.value[randomIndex], deck.value[currentIndex]]
  }

  return deck.value
}

const counter = () => {
 const active = setInterval(() => {
     
    if(start.value === false) {
      sec.value = '00'
      clearInterval(active)
    }

    if(sec.value === '00') {
        sec.value = 0
    }
    sec.value++
    if(sec.value < 10) {
        sec.value = `0${sec.value}`
    } else if(sec.value === 60) {
        min.value++
        sec.value = '00'
    } else {
        sec.value
    }
  },1000)
}
/*
const gamecheck = computed(() => {
  let minutes = time.minutes
  let total;

  minutes != 0 ? minutes = minutes * 60 : minutes = 0
  total = minutes + time.seconds
  
  if(total != 0 && redo.value != false) {
    if(total > 90) {
        setTimeout(() => {
            min.value = 0
            sec.value = '00'
        }, 3000)
      return "You have received the ranking of fífl!"
    } else if(total < 30) {
        setTimeout(() => {
            min.value = 0
            sec.value = '00'
        }, 3000)
      return "Oden's beard! You're a Viking Warlord!"
    } else {
        setTimeout(() => {
            min.value = 0
            sec.value = '00'
        }, 3000)
      return "You have some wits."
    }
  } else {
      return "Let's see how sharp your memory is!"
  }

})
*/

const gameEnds = () => {
  start.value = false
  redo.value = true
}

const startGame = () => {
  shuffle()
  start.value = true
  counter()
}

</script>

