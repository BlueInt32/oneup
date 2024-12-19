<script setup lang="ts">
import { onMounted, ref, type Ref } from 'vue';
import GameRow from './GameRow.vue';
import ValueOverlay from './ValueOverlay.vue';
const isSwipeActive = ref(false);
const currentCoordsActive = ref([null, null]) as Ref<Array<number | null>>;
const values = ref([]) as Ref<Array<Array<string>>>;
const overlayPositionX = ref('0');
const overlayPositionY = ref('0');
onMounted(() => {
  values.value = [
    ['1', '', '', '', ''],
    ['', '1', '', '', ''],
    ['', '', '1', '', ''],
    ['', '', '', '', ''],
    ['', '', '', '', ''],
  ];
});
function mouseDownHandler(event: MouseEvent, rowIndex: number, columnIndex: number) {
  isSwipeActive.value = true;
  currentCoordsActive.value = [rowIndex, columnIndex];
  console.log(event.x, event.y);
  overlayPositionX.value = `${event.x}px`;
  overlayPositionY.value = `${event.y}px`;
}

function overlayValueMouseUpHandler(value: number) {
  isSwipeActive.value = false;
  if (currentCoordsActive.value[0] === null || currentCoordsActive.value[1] === null) return;
  values.value[currentCoordsActive.value[0]][currentCoordsActive.value[1]] = '' + value;
}

function overlayClearMouseUpHandler() {
  isSwipeActive.value = false;
}
</script>

<template>
  <div
    v-if="isSwipeActive"
    class="overlay opacity-40 absolute top-0 left-0 z-40 w-full h-full bg-black"
  ></div>
  <ValueOverlay
    class="absolute w-72 ml-[-9rem] mt-[-5rem] h-auto bg-white z-50 flex flex-wrap"
    :style="{ left: overlayPositionX, top: overlayPositionY }"
    v-if="isSwipeActive"
    @value-mouseup="overlayValueMouseUpHandler"
    @clear-mouseup="overlayClearMouseUpHandler"
  ></ValueOverlay>
  <div class="flex justify-center" v-for="(row, index) in values" :key="index">
    <GameRow :row-index="index" @mouse-down="mouseDownHandler" :rowValues="row" />
  </div>
</template>
