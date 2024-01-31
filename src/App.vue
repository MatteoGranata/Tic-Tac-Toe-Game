<script setup lang="ts">
import { ref, reactive } from 'vue';
import Rules from './components/Rules.vue'

const winner = ref<string | null>(null);
const isTie = ref(false);
const gameover = ref(false);
const currentPlayer = ref('x');

const countX = ref(0)
const countO = ref(0)
const countDraw = ref(0)

let board = reactive([
  ['', '', ''],
  ['', '', ''],
  ['', '', '']
]);

const checkTie = () => {
  for (let i = 0; i < 3; i++) {
    for (let j = 0; j < 3; j++) {
      if (!board[i][j]) {
        return false;
      }
    }
  }
  return true;
}

const checkWin = () => {
  const a = currentPlayer.value;

  for (let i = 0; i < 3; i++) {
    if (board[i].every(cell => cell === a)) return true;
    if (board.every(row => row[i] === a)) return true;
  }

  if (board[0][0] === a && board[1][1] === a && board[2][2] === a) return true;
  if (board[0][2] === a && board[1][1] === a && board[2][0] === a) return true;

  return false;
};

const playMove = (row: number, col: number) => {
  if (!board[row][col] && !winner.value) {
    board[row][col] = currentPlayer.value;
    if (checkWin()) {
      winner.value = currentPlayer.value;
      if (winner.value == 'x') {
        countX.value++
      } else if (winner.value == 'o') {
        countO.value++
      }
    } else if (checkTie()) {
      isTie.value = true;
      countDraw.value++
    } else {
      currentPlayer.value = currentPlayer.value === 'x' ? 'o' : 'x';
    }
  }
}

const reset = () => {
  board = [
    ['', '', ''],
    ['', '', ''],
    ['', '', '']
  ];

  gameover.value = false;
  winner.value = null;
  isTie.value = false;

  if (currentPlayer.value == 'o') {
    currentPlayer.value = 'x'
  } else if (currentPlayer.value == 'x') {
    currentPlayer.value = 'o'
  }
}

const prompt = ref(currentPlayer)

</script>

<template>
  <div class="container-app">
    <div class="title-container">
      <h1 class="title">tic tac toe game</h1>
    </div>
    <div class="container-playing-player">
      <p class="playing-player"> current player: <span class="player"> {{ currentPlayer }}</span></p>
    </div>
    <div class="cell-container">
      <div class="row" v-for="(row, rowIndex) of board" :key="rowIndex">
        <div class="cell" v-for="(cell, cellIndex) of row" :key="cellIndex"
          :class="{ 'cell-x': cell === 'x', 'cell-o': cell === 'o' }" :disabled="cell !== null"
          @click="playMove(rowIndex, cellIndex)">
          {{ cell }}
        </div>
      </div>
    </div>
    <div class="score-container">
      <div class="score">player x has {{ countX }} point <br> draw {{ countDraw }} <br> player o have {{ countO }}
        points</div>
    </div>
    <div class="notify-container">
      <div class="notify">
        <p v-if="winner">{{ winner }} wins!</p>
        <p v-else-if="isTie">draw!</p>
      </div>
    </div>
      <div class="button-container">
        <button class="button" @click="reset">restart</button>
      </div>
  </div>
  <Rules :msg="prompt" />
</template>


