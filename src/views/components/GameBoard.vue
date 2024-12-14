<script setup lang="ts">
import GameRow from './GameRow.vue'
</script>

<template>
  <div class="flex" v-for="i in 5" :key="i">
    <GameRow class="flex" />
  </div>
</template>
