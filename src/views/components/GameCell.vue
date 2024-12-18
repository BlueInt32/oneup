<script setup lang="ts">
const emit = defineEmits(['mouse-down', 'mouse-up']);
const props = defineProps(['cellValue', 'rowIndex', 'columnIndex']);
function mouseDownHandler(event: MouseEvent) {
  if (event.button !== 0) return;
  emit('mouse-down', event, props.rowIndex, props.columnIndex);
}
function mouseUpHandler() {}
</script>

<template>
  <div
    @mousedown="mouseDownHandler"
    @mouseup="mouseUpHandler"
    class="flex w-32 h-32 text-6xl items-center justify-center border hover:bg-green-50 cursor-pointer select-none relative"
  >
    {{ props.cellValue }}
  </div>
</template>
