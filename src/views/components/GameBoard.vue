<script setup lang="ts">
import grids from '@/assets/grids.json';
import type { cellDescriptor } from '@/domain/cellDescriptor';
import { onMounted, ref, Transition, type Ref } from 'vue';
import GameRow from './GameRow.vue';
import ValueOverlay from './ValueOverlay.vue';

const isSwipeActive = ref(false);
const currentCoordsActive = ref([null, null]) as Ref<Array<number | null>>;
const values = ref([]) as Ref<Array<Array<cellDescriptor>>>;
const overlayPositionX = ref('0');
const overlayPositionY = ref('0');
const mainSize = ref(0);

onMounted(() => {
  const gridDescriptor = grids['g1'];

  mainSize.value = Number(gridDescriptor[0]);
  const cellsNumber = mainSize.value * mainSize.value;
  const preVals = gridDescriptor.substring(1, cellsNumber + 1);
  const cellsBorders = gridDescriptor.substring(
    1 + cellsNumber,
    1 + cellsNumber + (mainSize.value + 1) * (mainSize.value + 1) * 2,
  );
  for (let rowIndex = 0; rowIndex < mainSize.value; rowIndex++) {
    values.value.push([]);
    for (let colIndex = 0; colIndex < mainSize.value; colIndex++) {
      const preVal = Number(preVals[rowIndex * mainSize.value + colIndex]);
      const leftBorder =
        cellsBorders[rowIndex * (mainSize.value + 1) * 2 + colIndex * 2] === '0' ? false : true;
      const topBorder =
        cellsBorders[rowIndex * (mainSize.value + 1) * 2 + colIndex * 2 + 1] === '0' ? false : true;
      const val = preVal !== 0 ? preVal : null;
      values.value[rowIndex].push({
        preValue: val,
        currentValue: val,
        leftBorder: !!leftBorder,
        topBorder: !!topBorder,
      } as cellDescriptor);
    }
  }
  console.log(values.value);
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
  values.value[currentCoordsActive.value[0]][currentCoordsActive.value[1]].currentValue = value;
}

function overlayClearMouseUpHandler() {
  if (currentCoordsActive.value[0] === null || currentCoordsActive.value[1] === null) return;
  values.value[currentCoordsActive.value[0]][currentCoordsActive.value[1]].currentValue = null;
  isSwipeActive.value = false;
}
</script>

<template>
  <Transition>
    <div
      v-if="isSwipeActive"
      class="overlay opacity-30 absolute top-0 left-0 z-40 w-full h-full bg-black"
    ></div>
  </Transition>
  <Transition>
    <ValueOverlay
      :maxVal="mainSize"
      class="absolute w-72 ml-[-9rem] mt-[-5rem] h-auto bg-white z-50 flex flex-wrap"
      :style="{ left: overlayPositionX, top: overlayPositionY }"
      v-if="mainSize && isSwipeActive"
      @value-mouseup="overlayValueMouseUpHandler"
      @clear-mouseup="overlayClearMouseUpHandler"
    ></ValueOverlay>
  </Transition>
  <div class="flex justify-center" v-for="(row, index) in values" :key="index">
    <GameRow
      v-if="mainSize"
      :main-size="mainSize"
      :row-index="index"
      @mouse-down="mouseDownHandler"
      :rowValues="row"
    />
  </div>
</template>

<style scoped>
/* we will explain what these classes do next! */
.v-enter-active,
.v-leave-active {
  transition: opacity 0.15s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}
</style>
