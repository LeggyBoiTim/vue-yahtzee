<script setup>
const dice = defineModel();

const throwDice = () => {
    dice.value.length = 0;
    for (let i = 0; i < 5; i++) {
        const result = Math.floor(Math.random() * 6) + 1;
        dice.value.push(result);
    }
}
</script>

<template>
    <h1>Scoreblock</h1>
    <button @click="throwDice">Throw!</button>
    <table>
        <tr>
            <td v-for="(amount, index) in dice" :key="index">
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
