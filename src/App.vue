<script setup lang="ts">
import PlayerGame from './components/PlayerGame.vue'
import ControlGame from './components/ControlGame.vue'
import DiceGame from './components/DiceGame.vue'
import PopUpModal from './components/PopUpModal.vue'
import { ref } from 'vue'

const scorePlayer = ref<number[]>([13, 30])
const currentScore = ref<number>(0)
const activePlayer = ref<number>(0)
const isOpenPopup = ref(false)
const dices = ref([3, 4])
const isPlaying = ref(false)
const finalScore = ref<number>(100)
const isWinner = ref(false)
const handleNewGame = () => {
  console.log('fdfdfd')
  if (!finalScore.value || finalScore.value < 0) {
    alert('Please enter a valid final score greater than 0')
    return
  }
  isOpenPopup.value = !isOpenPopup.value
  console.log('isOpenPopup:', isOpenPopup.value)
}

const handleCloseModal = () => {
  isOpenPopup.value = false
}

const handleConfirm = () => {
  console.log('ban ra confirm vue')
  isPlaying.value = true
  isOpenPopup.value = false
  activePlayer.value = 0
  currentScore.value = 0
  scorePlayer.value = [0, 0]
  dices.value = [2, 2]
  isWinner.value = false
}

const handleRollDice = () => {
  if (isPlaying.value) {
    const dice1 = Math.floor(Math.random() * 6) + 1
    const dice2 = Math.floor(Math.random() * 6) + 1
    console.log(dice1, dice2)
    dices.value = [dice1, dice2]
    if (dice1 === 1 || dice2 === 1) {
      // Reset to 0
      currentScore.value = 0
      // switch to another player
      activePlayer.value = activePlayer.value === 0 ? 1 : 0
      alert(` Got 1! Switching to  another player: `)
    } else if (isPlaying.value && dice1 === dice2) {
      currentScore.value = currentScore.value + dice1 + dice2
      setTimeout(() => {
        alert(`Double ${dice1}! You get another turn!`)
      }, 300)
      console.log('Double! Current score:', currentScore.value)
    } else {
      currentScore.value += dice1 + dice2
      console.log('current +', currentScore.value)
    }
  } else {
    alert('Please click new game to start')
  }
}

const handleHoldScore = () => {
  console.log('ban hold score ra ngoai')
  if (isPlaying.value) {
    // add currentScore to Active Player
    scorePlayer.value[activePlayer.value] =
      scorePlayer.value[activePlayer.value] + currentScore.value
    console.log('currentScore', scorePlayer.value[activePlayer.value], scorePlayer.value)

    if (isWinner.value) {
      alert(`Game is over please start again`)
      return
    }
    // check if player has won or exceed finalScore
    if (scorePlayer.value[activePlayer.value] >= finalScore.value) {
      isWinner.value = true
      alert(`congratulations u won`)
      isPlaying.value = false
      return
    }
    currentScore.value = 0
    // Switch player
    activePlayer.value = activePlayer.value === 0 ? 1 : 0
  } else {
    alert('Please click new game to start')
  }
}

const updateFinalScore = (score: number) => {
  if (score > 0) {
    finalScore.value = score
  } else {
    alert('please enter valid score')
  }
}

const getPlayerName = (playerIndex: number): string => {
  if (isWinner.value && playerIndex === activePlayer.value) {
    return 'Winner !'
  }
  return `Player  ${playerIndex + 1}`
}
</script>

<template>
  <header>
    <h1>Dice game</h1>
  </header>

  <main>
    <div class="wrapper clearfix">
      <PlayerGame
        v-bind:scorePlayer="scorePlayer"
        v-bind:currentScore="currentScore"
        v-bind:activePlayer="activePlayer"
        v-bind:isWinner="isWinner"
        v-bind:getPlayerName="getPlayerName"
      />
      <ControlGame
        v-on:handleNewGame="handleNewGame"
        v-on:handleRollDice="handleRollDice"
        v-on:handleHoldScore="handleHoldScore"
        v-on:updateFinalScore="updateFinalScore"
        v-bind:isPlaying="isPlaying"
      />
      <DiceGame v-bind:activePlayer="activePlayer" v-bind:dices="dices" />
      <PopUpModal
        v-bind:isOpenPopup="isOpenPopup"
        v-on:handleConfirm="handleConfirm"
        v-on:closeModal="handleCloseModal"
      />
    </div>
  </main>
</template>

<style scoped>
.wrapper {
  width: 1000px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: #fff;
  box-shadow: 0px 10px 50px rgba(0, 0, 0, 0.3);
  overflow: hidden;
}
</style>
