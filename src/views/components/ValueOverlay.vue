<script setup lang="ts">
import OverlayCell from './OverlayCell.vue';
const emit = defineEmits(['value-mouseup', 'clear-mouseup']);
const props = defineProps(['maxVal']);

function valueMouseUpHandler(value: number) {
  emit('value-mouseup', value);
}
function clearMouseUpHandler() {
  emit('clear-mouseup');
}
</script>

<template>
  <div>
    <OverlayCell
      v-for="i in props.maxVal + 1"
      :key="i"
      :val="i < props.maxVal + 1 ? i : '❌'"
      @value-mouseup="valueMouseUpHandler"
      @clear-mouseup="clearMouseUpHandler"
    />
  </div>
</template>
