<script setup lang="ts">
import GameCell from './GameCell.vue'
</script>

<template>
  <div class="flex" v-for="i in 5" :key="i">
    <GameCell class="flex" />
  </div>
</template>

<style scoped></style>
