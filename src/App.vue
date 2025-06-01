<script setup>
import BaceButton from './components/BaceButton.vue'
import { ref } from 'vue'
const playerChoice = ref('') // выбор игрока
const opponentChoice = ref('')
const resultYou = ref(0)
const resultOpp = ref(0)
const gameResult = ref('')

const handlePlayerChoice = (choice) => {
  playerChoice.value = choice

  const choices = ['rock', 'scissors', 'paper']
  opponentChoice.value = choices[Math.floor(Math.random() * 3)]
  resultTim()
}
const resetGame = () => {
  playerChoice.value = ''
  opponentChoice.value = ''
  gameResult.value = 'Start play'
  resultYou.value = 0
  resultOpp.value = 0
}

const resultTim = () => {
  const p = playerChoice.value
  const o = opponentChoice.value
  if (p === o) {
    gameResult.value = 'Draw'
    return
  }

  if (
    (p === 'rock' && o === 'scissors') ||
    (p === 'scissors' && o === 'paper') ||
    (p === 'paper' && o === 'rock')
  ) {
    gameResult.value = 'You won'
    resultYou.value++
  } else {
    gameResult.value = 'You lost'
    resultOpp.value++
  }
}
</script>
<template>
  <header>
    <h1 class="title">ROCKPAPERSCISSORS</h1>

    <div class="counters">
      <div class="counter">{{ resultYou }}</div>
      <div class="counter">{{ resultOpp }}</div>
    </div>

    <div class="choice">
      <div class="choice-label">your choice</div>
      <div class="choice-label">choice of opponent</div>
    </div>
    <div class="choice-look">
      <BaceButton form="square" :img="playerChoice || 'rock'" color="grey"></BaceButton>
      <BaceButton form="square" :img="opponentChoice || 'scissors'" color="grey"></BaceButton>
    </div>
    <div class="result" v-if="gameResult">
      <BaceButton form="rectangle" :text="'RESULT: ' + gameResult" color="pink"></BaceButton>
    </div>
    <div class="button-click">
      <BaceButton
        form="square"
        img="rock"
        color="green"
        @click="handlePlayerChoice('rock')"
      ></BaceButton>

      <BaceButton
        form="square"
        img="scissors"
        color="green"
        @click="handlePlayerChoice('scissors')"
      ></BaceButton>

      <BaceButton
        form="square"
        img="paper"
        color="green"
        @click="handlePlayerChoice('paper')"
      ></BaceButton>
    </div>
    <div class="finish">
      <BaceButton form="rectangle" text="reset-game" color="pink" @click="resetGame"></BaceButton>
    </div>
  </header>
</template>

<style scoped>
body {
  margin: 0;
  padding: 0;
  min-height: 100vh;
}

header {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 20px 0;
  box-sizing: border-box;
  z-index: 100;
  height: 180px;
}

.title {
  color: #db7093;
  margin: 0 0 20px 0;
  font-family: 'Times New Roman', Times, serif;
  font-size: 38px;
  text-align: center;
  width: 100%;
}

.counters {
  display: flex;
  justify-content: center;
  gap: 100px;
  width: 100%;
  font-family: 'Times New Roman', Times, serif;
  font-size: 50px;
}

.counter {
  min-width: 60px;
  text-align: center;
}

.choice {
  display: flex;
  justify-content: center;
  gap: 100px;
  width: 100%;
  font-family: 'Times New Roman', Times, serif;
  font-size: 35px;
  margin-top: 20px;
}

.choice-label {
  min-width: 200px;
  text-align: center;
}
.button-click,
.finish {
  display: flex;
  justify-content: center;
  gap: 100px;
  width: 100%;
  font-size: 35px;
  margin-top: 20px;
}
.choice-look {
  display: flex;
  justify-content: center;
  gap: 100px;
  width: 100%;
  font-size: 35px;
  margin-top: 20px;
}
.result {
  display: flex;
  justify-content: center;
  gap: 100px;
  width: 100%;
  font-size: 35px;
  margin-top: 20px;
}
</style>
