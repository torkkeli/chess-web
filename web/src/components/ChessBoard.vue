<script setup lang="ts">
import { ref } from 'vue'
import MoveList from './MoveList.vue'
import ChessSquare from './ChessSquare.vue'

const files = ['a','b','c','d','e','f','g','h']
const ranks = [8,7,6,5,4,3,2,1]
const board = [
  ['r','n','b','q','k','b','n','r'],
  ['p','p','p','p','p','p','p','p'],
  ['','','','','','','',''],
  ['','','','','','','',''],
  ['','','','','','','',''],
  ['','','','','','','',''],
  ['P','P','P','P','P','P','P','P'],
  ['R','N','B','Q','K','B','N','R']
]
const moves = ['e4', 'e5', 'Nf3', 'Nc6', 'Bb5', 'a6']
const selectedSquare = ref<{ square: typeof ChessSquare | null } | null>(null)
const turn = ref<'w' | 'b'>('w')

</script>

<template>
  <div class="board-layout">
    <div class="board-wrapper">
      <div class="ranks-files">
        <div class="ranks">
          <span v-for="rank in ranks" :key="rank">{{ rank }}</span>
        </div>
        <div class="chess-board">
          <ChessSquare
            v-for="(piece, idx) in board.flat()"
            :key="`${Math.floor(idx / 8)}-${idx % 8}`"
            :rank="Math.floor(idx / 8)"
            :file="idx % 8"
            :piece="piece"
          />
        </div>
      </div>
      <div class="files">
        <span v-for="file in files" :key="file">{{ file }}</span>
      </div>
    </div>
    <MoveList :moves="moves" />
  </div>
</template>

<style scoped>
.board-layout {
  display: flex;
  flex-direction: row;
  align-items: flex-start;
  justify-content: center;
  gap: 2rem;
}

.board-wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 1rem;
  background: #333;
  border-radius: 1rem;
  border: 4px solid #333;
  width: fit-content;
  margin: auto;
}

.files {
  display: grid;
  grid-template-columns: repeat(8, 1fr);
  width: 80vw;
  max-width: 600px;
  margin-bottom: 4px;
}

.files span {
  color: #fff;
  text-align: center;
  font-weight: bold;
  font-size: 1.2rem;
}

.ranks-files {
  display: flex;
  flex-direction: row;
}

.ranks {
  display: grid;
  grid-template-rows: repeat(8, 1fr);
  margin-right: 4px;
  height: 80vw;
  max-height: 600px;
}

.ranks span {
  color: #fff;
  display: flex;
  align-items: center;
  height: 100%;
  font-weight: bold;
  font-size: 1.2rem;
}

.chess-board {
  display: grid;
  grid-template-columns: repeat(8, 1fr);
  grid-template-rows: repeat(8, 1fr);
  width: 80vw;
  max-width: 600px;
  aspect-ratio: 1 / 1;
}
</style>