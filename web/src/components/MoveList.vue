<script setup lang="ts">
import { computed } from 'vue'

const props = defineProps<{
  moves: string[]
}>()

const movePairs = computed(() => {
  const pairs = []
  for (let i = 0; i < props.moves.length; i += 2) {
    pairs.push([props.moves[i], props.moves[i + 1]])
  }
  return pairs
})
</script>

<template>
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
</template>

<style scoped>
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