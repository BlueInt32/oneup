<script setup lang="ts">
import { ref } from 'vue';
import OverlayCell from './OverlayCell.vue';
const emit = defineEmits(['value-mouseup', 'clear-mouseup']);
const val = ref(1);
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
      v-for="i in 5"
      :key="i"
      :val="i < 10 ? i : '❌'"
      @value-mouseup="valueMouseUpHandler"
      @clear-mouseup="clearMouseUpHandler"
    />
  </div>
</template>
