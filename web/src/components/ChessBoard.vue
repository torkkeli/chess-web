<script setup lang="ts">
import { computed } from 'vue'
import bR from '@/assets/pieces/bR.svg'
import bN from '@/assets/pieces/bN.svg'
import bB from '@/assets/pieces/bB.svg'
import bQ from '@/assets/pieces/bQ.svg'
import bK from '@/assets/pieces/bK.svg'
import bP from '@/assets/pieces/bP.svg'
import wR from '@/assets/pieces/wR.svg'
import wN from '@/assets/pieces/wN.svg'
import wB from '@/assets/pieces/wB.svg'
import wQ from '@/assets/pieces/wQ.svg'
import wK from '@/assets/pieces/wK.svg'
import wP from '@/assets/pieces/wP.svg'

const files = ['a','b','c','d','e','f','g','h']
const ranks = [8,7,6,5,4,3,2,1]
const pieces: Record<string, string> = {
  r: bR,
  n: bN,
  b: bB,
  q: bQ,
  k: bK,
  p: bP,
  R: wR,
  N: wN,
  B: wB,
  Q: wQ,
  K: wK,
  P: wP,
  '': ''
}
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

function getSquareColor(row: number, col: number) {
  return (row + col) % 2 === 0 ? 'white' : 'black'
}

const movePairs = computed(() => {
  const pairs = []
  for (let i = 0; i < moves.length; i += 2) {
    pairs.push([moves[i], moves[i + 1]])
  }
  return pairs
})
</script>

<template>
  <div class="board-layout">
    <div class="board-wrapper">
      <div class="ranks-files">
        <div class="ranks">
          <span v-for="rank in ranks" :key="rank">{{ rank }}</span>
        </div>
        <div class="chess-board">
          <div
            v-for="(piece, idx) in board.flat()"
            :key="idx"
            class="chess-square"
            :class="getSquareColor(Math.floor(idx / 8), idx % 8)"
          >
            <img
              v-if="piece"
              :src="pieces[piece]"
              alt=""
              class="piece-img"
            />
          </div>
        </div>
      </div>
      <div class="files">
        <span v-for="file in files" :key="file">{{ file }}</span>
      </div>
    </div>
    <div class="move-list">
      <h3>Moves</h3>
      <table class="moves-table">
        <tbody>
          <tr v-for="(movePair, idx) in movePairs" :key="idx">
            <td class="move-num">{{ idx + 1 }}.</td>
            <td class="move-white">{{ movePair[0] || '' }}</td>
            <td class="move-black">{{ movePair[1] || '' }}</td>
          </tr>
        </tbody>
      </table>
    </div>
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

.chess-square {
  width: 100%;
  height: 100%;
}

.chess-square.white {
  background: #e6cfa7;
}

.chess-square.black {
  background: #9d5502;
}

.piece {
  font-size: 2.5vw;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
  user-select: none;
}

.piece-img {
  width: 90%;
  height: 90%;
  object-fit: contain;
  pointer-events: none;
  user-select: none;
  display: block;
  margin: auto;
}

.move-list {
  background: #222;
  color: #fff;
  border-radius: 1rem;
  border: 2px solid #333;
  padding: 1rem;
  min-width: 150px;
  max-height: 600px;
  overflow-y: auto;
  margin-top: 0;
}

.move-list h3 {
  margin-top: 0;
  margin-bottom: 1rem;
  font-size: 1.2rem;
  text-align: center;
}

.moves-table {
  width: 100%;
  border-collapse: collapse;
}

.moves-table td {
  padding: 0.25rem 0.5rem;
  border-bottom: 1px solid #444;
  font-family: monospace;
  text-align: left;
}

.move-num {
  color: #aaa;
  width: 2rem;
  text-align: right;
}

.move-white, .move-black {
  width: 4rem;
}
</style>