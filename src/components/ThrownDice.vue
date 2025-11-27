<script setup>
import { ref } from 'vue';

const diceArray = defineModel();
const diceCount = ref({
    1: 0,
    2: 0,
    3: 0,
    4: 0,
    5: 0,
    6: 0
});

const throwDice = () => {
    diceArray.value = [];
    diceCount.value = {1: 0, 2: 0, 3: 0, 4: 0, 5: 0, 6: 0};
    for (let i = 0; i < 5; i++) {
        const result = Math.floor(Math.random() * 6) + 1;
        diceArray.value.push(result);
        diceCount.value[result]++;
    }
    console.log(diceArray.value, diceCount.value);
}
</script>

<template>
    <h1>Scoreblock</h1>
    <button @click="throwDice">Throw!</button>
    <table>
        <tr>
            <td v-for="(amount, index) in diceArray" :key="index">
                <p>{{ amount }}</p>
            </td>
        </tr>
    </table>
</template>

<style scoped>
table {
    border-collapse: separate;
    border: black 5px solid;
    border-radius: 10px;
    table-layout: fixed;
    width: 400px;
    height: 80px;
}

td {
    border-left:solid black 2px;
    font-size: xx-large;
    font-weight: bold;
    line-height: 0;
}

td:first-child {
    border-left: none;
}
</style>
