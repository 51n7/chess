<script setup lang="ts">
const props = defineProps<{
  selectedSquare: string | null
}>()

const emit = defineEmits<{
  squareClick: [squareId: string]
}>()

const boardSize = 8

const isLightSquare = (row: number, col: number): boolean => {
  return (row + col) % 2 === 0
}

const getSquareId = (row: number, col: number): string => {
  const colLetter = String.fromCharCode(97 + col) // a-h
  return `${colLetter}${row + 1}`
}

const handleSquareClick = (row: number, col: number) => {
  const squareId = getSquareId(row, col)
  emit('squareClick', squareId)
}

const isSelected = (row: number, col: number): boolean => {
  return props.selectedSquare === getSquareId(row, col)
}
</script>

<template>
  <div class="chessboard-container">
    <div class="chessboard">
      <div
        v-for="row in boardSize"
        :key="row"
        class="board-row"
      >
        <div
          v-for="col in boardSize"
          :key="col"
          :class="[
            'square',
            isLightSquare(row - 1, col - 1) ? 'light' : 'dark',
            isSelected(row - 1, col - 1) ? 'selected' : ''
          ]"
          @click="handleSquareClick(row - 1, col - 1)"
        >
          <span class="square-label">{{ getSquareId(row - 1, col - 1) }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>

.chessboard-container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-width: 0;
  flex: 1;
}

.chessboard {
  display: flex;
  flex-direction: column;
  align-self: center;
  box-shadow: var(--shadow-md);
  border: 1px solid var(--color-border-secondary);
  gap: 0;
  border-radius: 10px;
  overflow: hidden;
  width: 100%;
  max-width: 480px;
  aspect-ratio: 1;
}

.board-row {
  display: flex;
  gap: 0;
  flex: 1;

  &:first-child {

    /* Top-left corner */
    .square:first-child.selected,
    .square:first-child:hover {
      border-top-left-radius: 10px;
    }

    /* Top-right corner */
    .square:last-child.selected,
    .square:last-child:hover {
      border-top-right-radius: 10px;
    }
  }

  &:last-child {

    /* Bottom-left corner */
    .square:first-child.selected,
    .square:first-child:hover {
      border-bottom-left-radius: 10px;
    }

    /* Bottom-right corner */
    .square:last-child.selected,
    .square:last-child:hover {
      border-bottom-right-radius: 10px;
    }
  }
}

.square {
  flex: 1;
  aspect-ratio: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  cursor: pointer;
  transition: all 0.2s ease;

  &.light {
    background-color: var(--color-square-light);
  }

  &.dark {
    background-color: var(--color-square-dark);
  }

  &:hover {
    z-index: 1;
    box-shadow: var(--shadow-hover), inset 0 0 0 1px var(--color-border-hover);
  }

  &.selected {
    background-color: var(--color-square-selected);
    box-shadow: inset 0 0 0 2px var(--color-square-selected-border);
  }
}

.square-label {
  position: absolute;
  top: 2px;
  left: 4px;
  font-size: clamp(8px, 1.5vw, 10px);
  font-weight: 600;
  color: var(--color-label);
  pointer-events: none;
}

@media (min-width: 1024px) {
  .chessboard {
    max-width: 640px;
  }
}
</style>
