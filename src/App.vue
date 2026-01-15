<script setup lang="ts">
import { ref } from 'vue'
import ChessBoard from './components/ChessBoard.vue'
import SideBar from './components/SideBar.vue'

const selectedSquare = ref<string | null>(null)
const clickedSquares = ref<string[]>([])

const handleSquareClick = (squareId: string) => {
  selectedSquare.value = squareId
  clickedSquares.value.unshift(squareId)
}

const handleClearMoves = () => {
  clickedSquares.value = []
}
</script>

<template>
  <div class="container">
    <ChessBoard
      :selected-square="selectedSquare"
      @square-click="handleSquareClick"
    />

    <SideBar
      :selected-square="selectedSquare"
      :clicked-squares="clickedSquares"
      @clear-moves="handleClearMoves"
    />
  </div>
</template>

<style scoped>

.container {
  max-width: 1200px;
  min-width: 280px;
  width: 87.5%;
  margin-inline: auto;
  display: flex;
  flex-direction: column;
  gap: 20px;
  padding-block: 20px;
}

.app-container {
  display: flex;
  flex-direction: column;
  padding: 10px;
  gap: 10px;
  background: var(--color-bg-primary);
}

.main-content {
  flex: 1;
  display: flex;
  justify-content: center;
  align-items: center;
  min-width: 0;
}

@media (min-width: 1024px) {
  .app-container {
    height: 100%;
    flex-direction: row;
    padding: 20px;
    gap: 20px;
  }

  .container {
    flex-direction: row;
  }
}

</style>
