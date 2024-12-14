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
  <div class="absolute left-[50%] ml-[-12rem] w-72 h-72 bg-white z-50 flex flex-wrap">
    <OverlayCell
      v-for="i in 10"
      :key="i"
      :val="i < 10 ? i : '❌'"
      @value-mouseup="valueMouseUpHandler"
      @clear-mouseup="clearMouseUpHandler"
    />
  </div>
</template>
