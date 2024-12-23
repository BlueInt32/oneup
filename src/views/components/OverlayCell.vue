<script setup lang="ts">
import { onMounted } from 'vue';

const props = defineProps(['val']);
const emit = defineEmits(['value-mouseup', 'clear-mouseup']);
onMounted(() => {
  console.log(props.val);
});
function mouseUpHandler(value: any) {
  if (value === '❌') {
    emit('clear-mouseup');
  } else {
    emit('value-mouseup', value);
  }
}
</script>

<template>
  <div
    @mouseup="mouseUpHandler(props.val)"
    class="flex w-24 h-24 text-5xl items-center justify-center border bg-white hover:bg-green-50 cursor-pointer select-none relative"
  >
    {{ props.val }}
  </div>
</template>
