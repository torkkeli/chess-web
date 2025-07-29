<script setup lang="ts">
import ChessBoard from './components/ChessBoard.vue'
</script>

<template>
  <div class="board">
    <ChessBoard />
  </div>
</template>

<style scoped>
.app-container {
  min-height: 100vh;
  display: 100vw;
  flex-direction: relative;
}

.board {
  flex: 1;
  display: flex;
  justify-content: center;
  align-items: center;
  box-sizing: border-box;
}

/* Add space for the logo only on small screens */
@media (max-width: 600px) {
  .board {
    margin-top: 8rem;
    margin-left: 8rem;
  }
}
</style>
