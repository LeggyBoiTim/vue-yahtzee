<script setup>
import { ref } from 'vue';
import ThrownDice from './components/ThrownDice.vue';
import ScoreTable from './components/ScoreTable.vue';
</script>

<template>
  <div id="app">
    <ThrownDice />
    <ScoreTable />
  </div>
</template>

<style scoped>
</style>
