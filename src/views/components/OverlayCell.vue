<script setup lang="ts">
const props = defineProps(['val']);
const emit = defineEmits(['value-mouseup', 'clear-mouseup']);
function mouseUpHandler(value: any) {
  if (value === '❌') {
    console.log('clear');
    emit('clear-mouseup');
  } else {
    emit('value-mouseup', value);
  }
}
</script>

<template>
  <div
    @mouseup="mouseUpHandler(props.val)"
    class="flex w-24 h-24 text-5xl items-center justify-center border hover:bg-green-50 cursor-pointer select-none relative"
  >
    {{ props.val }}
  </div>
</template>
