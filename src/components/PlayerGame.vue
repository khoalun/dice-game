<script setup lang="ts">
import { defineProps, type PropType } from 'vue'

defineProps({
  scorePlayer: {
    type: Array as PropType<number[]>,
    default: () => [0, 0],
  },
  currentScore: {
    type: Number,
    default: 0,
  },
  activePlayer: {
    type: Number,
    default: 0,
  },
  isWinner: {
    type: Boolean,
    default: false,
  },
  getPlayerName: {
    type: Function as PropType<(index: number) => string>,
    required: true,
  },
})
</script>

<template>
  <div class="item">
    <div
      class="player-panel"
      v-bind:class="{ active: activePlayer === 0 && !isWinner, winner: !activePlayer && isWinner }"
    >
      <div class="player-name">{{ getPlayerName(0) }}</div>
      <div class="player-score">{{ scorePlayer[0] }}</div>
      <div class="player-current-box">
        <div class="player-current-label">Current</div>
        <div class="player-current-score">{{ activePlayer == 0 ? currentScore : 0 }}</div>
      </div>
    </div>

    <div
      class="player-panel"
      v-bind:class="{ active: activePlayer == 1, winner: !activePlayer && isWinner }"
    >
      <div class="player-name">{{ getPlayerName(1) }}</div>
      <div class="player-score">{{ scorePlayer[1] }}</div>
      <div class="player-current-box">
        <div class="player-current-label">Current</div>
        <div class="player-current-score">{{ activePlayer == 1 ? currentScore : 0 }}</div>
      </div>
    </div>
  </div>
</template>

<style scoped>
/**********************************************
*** PLAYERS
**********************************************/
.player-panel {
  width: 50%;
  float: left;
  height: 600px;
  padding: 100px;
  transition: all 0.3s ease;
  background-color: #fff;
}
.player-name {
  font-size: 40px;
  text-align: center;
  text-transform: uppercase;
  letter-spacing: 2px;
  font-weight: 100;
  margin-top: 20px;
  margin-bottom: 10px;
  position: relative;
}

.player-score {
  text-align: center;
  font-size: 80px;
  font-weight: 100;
  color: #42b983;
  margin-bottom: 130px;
}

.active {
  background-color: #f7f7f7;
}
.active .player-name {
  font-weight: 300;
}

.active .player-name::after {
  content: '\2022';
  font-size: 47px;
  position: absolute;
  color: #42b983;
  top: -7px;
  right: 10px;
}

.player-current-box {
  background-color: #42b983;
  color: #fff;
  width: 40%;
  margin: 0 auto;
  padding: 12px;
  text-align: center;
}

.player-current-label {
  text-transform: uppercase;
  margin-bottom: 10px;
  font-size: 12px;
  color: #222;
}

.player-current-score {
  font-size: 30px;
}

.winner {
  background-color: #f7f7f7;
}
.winner .player-name {
  font-weight: 300;
  color: #42b983;
}
</style>
