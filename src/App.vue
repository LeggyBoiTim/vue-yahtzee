<script setup>
import { ref } from 'vue';
import ThrownDice from './components/ThrownDice.vue';
import ScoreTable from './components/ScoreTable.vue';

const dice = ref([]);
</script>

<template>
  <div id="app">
    <ThrownDice v-model="dice"/>
    <ScoreTable v-model="dice"/>
  </div>
</template>

<style scoped>
</style>
