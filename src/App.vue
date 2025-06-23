<script setup>
import BaseButton from './components/BaseButton.vue'
import Counter from './components/Counter.vue'
import { computed, ref } from 'vue'
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
const buttons = [
  { id: 1, img: 'rock', choice: 'rock' },
  { id: 2, img: 'scissors', choice: 'scissors' },
  { id: 3, img: 'paper', choice: 'paper' },
]
const looks = computed(() => [
  { id: 'player', img: playerChoice.value || 'rock' },
  { id: 'opponent', img: opponentChoice.value || 'scissors' },
])
</script>
<template>
  <header>
    <h1 class="title">ROCKPAPERSCISSORS</h1>

    <Counter :result-you="resultYou" :result-opp="resultOpp"> </Counter>
    <div class="choice">
      <div class="choice-label">your choice</div>
      <div class="choice-label">choice of opponent</div>
    </div>

    <div class="choice-look">
      <BaseButton
        v-for="look in looks"
        :key="look.id"
        form="square"
        :img="look.img"
        color="grey"
      ></BaseButton>
    </div>

    <div class="result" v-if="gameResult">
      <BaseButton form="rectangle" :text="'RESULT: ' + gameResult" color="pink"></BaseButton>
    </div>

    <div class="button-click">
      <BaseButton
        v-for="button in buttons"
        :key="button.id"
        form="square"
        :img="button.img"
        color="green"
        @click="handlePlayerChoice(button.choice)"
      ></BaseButton>
    </div>
    <div class="finish">
      <BaseButton form="rectangle" text="reset-game" color="pink" @click="resetGame"></BaseButton>
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
