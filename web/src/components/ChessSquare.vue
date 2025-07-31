<script setup lang="ts">
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
const props = defineProps<{
    rank: number,
    file: number,
    piece: string | null
}>()

function getSquareColor(rank: number, file: number) {
  return (rank + file) % 2 === 0 ? 'white' : 'black'
}
</script>

<template>
    <div
    :key="`${props.rank}-${props.file}`"
    class="chess-square"
    :class="getSquareColor(props.rank, props.file)"
    >
    <img
        v-if="piece"
        :src="pieces[piece]"
        alt=""
        class="piece-img"
    />
    </div>
</template>

<style scoped>
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
</style>