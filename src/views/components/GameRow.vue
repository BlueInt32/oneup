<script setup lang="ts">
import GameCell from './GameCell.vue';

const emit = defineEmits(['mouse-down', 'mouse-up']);
const props = defineProps(['mainSize', 'rowValues', 'rowIndex']);
function mouseDownHandler(event: MouseEvent, rowIndex: number, columnIndex: number) {
  emit('mouse-down', event, rowIndex, columnIndex);
}
</script>

<template>
  <div
    class="flex border-black"
    :class="{
      'border-t-8': props.rowIndex === 0,
      'border-b-8': props.rowIndex === props.mainSize - 1,
    }"
    v-for="(val, index) in props.rowValues"
    :key="index"
  >
    <GameCell
      :row-index="props.rowIndex"
      :column-index="index"
      :cellValue="val"
      :main-size="props.mainSize"
      @mouse-down="mouseDownHandler"
      @mouse-up="emit('mouse-up')"
    />
  </div>
</template>

<style scoped></style>
