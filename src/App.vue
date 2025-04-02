<script setup lang="ts">
import PlayerGame from './components/PlayerGame.vue'
import ControlGame from './components/ControlGame.vue'
import DiceGame from './components/DiceGame.vue'
import { ref } from 'vue'

const scorePlayer = ref<number[]>([13, 30])
</script>

<template>
  <header>
    <h1>Dice game</h1>
  </header>

  <main>
    <div class="wrapper clearfix">
      <PlayerGame v-bind:scorePlayer="scorePlayer" />
      <ControlGame />
      <DiceGame />
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
