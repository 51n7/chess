<script setup lang="ts">
defineProps<{
  selectedSquare: string | null
  clickedSquares: string[]
}>()

const emit = defineEmits<{
  clearMoves: []
}>()

const handleClear = () => {
  emit('clearMoves')
}
</script>

<template>
  <aside class="sidebar">
    <h2>Game Info</h2>
    <div class="sidebar-content">
      <div class="info-section">
        <h3>Selected Square</h3>
        <p v-if="selectedSquare" class="selected-info">{{ selectedSquare }}</p>
        <p v-else class="no-selection">Click a square to select</p>
      </div>

      <div class="info-section">
        <h3>Moves</h3>
        <div class="moves-list">
          <p v-if="clickedSquares.length === 0" class="empty-state">
            No moves yet
          </p>
          <ol v-else class="moves">
            <li
              v-for="(square, index) in clickedSquares"
              :key="index"
              class="move-item"
            >
              <span class="move-number">{{ clickedSquares.length - index }}.</span>
              <span class="move-square">{{ square }}</span>
            </li>
          </ol>
        </div>
        <button
          v-if="clickedSquares.length > 0"
          class="clear-button"
          @click="handleClear"
        >
          Clear Moves
        </button>
      </div>
    </div>
  </aside>
</template>

<style scoped>
.sidebar {
  background: var(--color-bg-secondary);
  border-radius: 8px;
  box-shadow: var(--shadow-sm);
  padding: 24px;
  display: flex;
  flex-direction: column;

  h2 {
    margin: 0 0 20px 0;
    color: var(--color-text-primary);
    font-size: 24px;
    border-bottom: 2px solid var(--color-border-primary);
    padding-bottom: 12px;
  }
}

.sidebar-content {
  display: flex;
  flex-direction: column;
  gap: 24px;
}

.info-section {
  background: var(--color-bg-tertiary);
  padding: 16px;
  border-radius: 6px;
  border: 1px solid var(--color-border-primary);

  h3 {
    margin: 0 0 12px 0;
    color: var(--color-text-secondary);
    font-size: 16px;
    font-weight: 600;
  }

  p {
    margin: 0;
    color: var(--color-text-tertiary);
    font-size: 14px;
  }
}

.selected-info {
  font-weight: 600;
  color: var(--color-primary) !important;
  font-size: 18px !important;
}

.no-selection {
  font-style: italic;
  color: var(--color-text-muted) !important;
}

.moves-list {
  max-height: 290px;
  overflow-y: auto;
}

.empty-state {
  color: var(--color-text-muted);
  font-style: italic;
}

.moves {
  margin: 0;
  padding: 0;
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.move-item {
  display: flex;
  align-items: center;
  gap: 8px;
  padding: 8px;
  background: var(--color-bg-secondary);
  border-radius: 4px;
  border: 1px solid var(--color-border-primary);
  transition: background-color 0.2s ease;

  &:hover {
    background-color: var(--color-bg-hover);
  }
}

.move-number {
  font-weight: 600;
  color: var(--color-text-light);
  min-width: 24px;
}

.move-square {
  font-weight: 600;
  color: var(--color-primary);
  font-family: monospace;
}

.clear-button {
  width: 100%;
  margin-top: 12px;
  padding: 10px 16px;
  background-color: var(--color-danger);
  color: var(--color-text-inverse);
  border: none;
  border-radius: 6px;
  font-size: 14px;
  font-weight: 600;
  cursor: pointer;
  transition: background-color 0.2s ease, transform 0.1s ease;

  &:hover {
    background-color: var(--color-danger-hover);
  }

  &:active {
    transform: scale(0.98);
  }
}

@media (min-width: 1024px) {
  .sidebar {
    min-width: 360px;
  }
}

</style>
