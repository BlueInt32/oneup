<script setup lang="ts">
import { ref, type Ref } from 'vue';
import CellOverlay from './CellOverlay.vue';
const val = ref(1) as Ref<number | string>;
const isSwipeActive = ref(false);
function mouseDownHandler() {
  isSwipeActive.value = true;
}
function mouseUpHandler() {}
function overlayValueMouseUpHandler(value: number) {
  isSwipeActive.value = false;
  val.value = value;
}
function overlayClearMouseUpHandler() {
  isSwipeActive.value = false;
  val.value = '';
}
</script>

<template>
  <div
    @mousedown="mouseDownHandler"
    @mouseup="mouseUpHandler"
    class="flex w-40 h-40 text-7xl items-center justify-center border hover:bg-green-50 cursor-pointer select-none relative"
  >
    {{ val }}
    <CellOverlay
      v-if="isSwipeActive"
      @value-mouseup="overlayValueMouseUpHandler"
      @clear-mouseup="overlayClearMouseUpHandler"
    ></CellOverlay>
  </div>
</template>
