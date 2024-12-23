<script setup lang="ts">
const emit = defineEmits(['mouse-down', 'mouse-up']);
const props = defineProps(['mainSize', 'cellValue', 'rowIndex', 'columnIndex']);
function mouseDownHandler(event: MouseEvent) {
  if (event.button !== 0) return;
  emit('mouse-down', event, props.rowIndex, props.columnIndex);
}
function mouseUpHandler() {}
//  :class="{
//   'border-l-[0.7rem]': props.cellValue.leftBorder,
//   'border-t-[0.7rem]': props.cellValue.topBorder,
//   'border-r-[0.7rem]': props.columnIndex + 1 === props.mainSize,
//   'border-b-[0.7rem]': props.rowIndex + 1 === props.mainSize,
// }"
</script>

<template>
  <div
    @mousedown="mouseDownHandler"
    @mouseup="mouseUpHandler"
    class="flex border-black w-32 h-32 text-6xl items-center justify-center border hover:bg-green-50 border-black cursor-pointer select-none relative"
    :class="{
      'border-l-8': props.columnIndex === 0,
      'border-r-8': props.columnIndex === props.mainSize - 1,
    }"
  >
    <div
      v-if="
        props.cellValue.leftBorder &&
        props.columnIndex !== 0 &&
        props.columnIndex !== props.mainSize - 1
      "
      class="absolute w-2 h-32 bg-black left-[-0.25rem] rounded"
    />
    <div
      v-if="
        props.cellValue.topBorder && props.rowIndex !== 0 && props.rowIndex !== props.mainSize - 1
      "
      class="absolute w-32 h-2 bg-black top-[-0.25rem] rounded"
    />
    {{ props.cellValue.currentValue }}
  </div>
</template>
