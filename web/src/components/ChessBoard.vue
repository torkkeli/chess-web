<script setup lang="ts">
const rows = 8
const cols = 8

function getSquareColor(row: number, col: number) {
  return (row + col) % 2 === 0 ? 'white' : 'black'
}
</script>

<template>
  <div class="chess-board">
    <div
      v-for="row in rows"
      :key="row"
      class="chess-row"
    >
      <div
        v-for="col in cols"
        :key="col"
        class="chess-square"
        :class="getSquareColor(row - 1, col - 1)"
      ></div>
    </div>
  </div>
</template>

<style scoped>
.chess-board {
  display: inline-block;
  border: 2px solid #333;
}
.chess-row {
  display: flex;
}
.chess-square {
  width: 40px;
  height: 40px;
}
.chess-square.white {
  background: #e6cfa7;
}
.chess-square.black {
  background: #4a2f11;
}
</style>