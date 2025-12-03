<script setup>
import { computed, ref, watch } from 'vue';

const dice = defineModel();

const diceCount = ref({
    1: '',
    2: '',
    3: '',
    4: '',
    5: '',
    6: ''
});

watch(dice.value, () => {
    diceCount.value = {1: '', 2: '', 3: '', 4: '', 5: '', 6: ''};
    for (const die of dice.value) {
        diceCount.value[die]++;
    }
});

const onesToSixes = computed(() => {
    const object = {};
    for (const face in diceCount.value) {
        diceCount.value[face] ? object[face] = face * diceCount.value[face] : object[face] == '';
    }
    return object;
});
</script>

<template>
    <table>
        <thead>
            <tr>
                <th>Part 1</th>
                <td>Score</td>
                <td>Game 1</td>
                <td>Game 2</td>
                <td>Game 3</td>
                <td>Game 4</td>
                <td>Game 5</td>
                <td>Game 6</td>
            </tr>
        </thead>
        <tbody>
            <tr>
                <th>Ones</th>
                <td>Total 1's</td>
                <td>{{ onesToSixes[1] }}</td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
            </tr>
            <tr>
                <th>Twos</th>
                <td>Total 2's</td>
                <td>{{ onesToSixes[2] }}</td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
            </tr>
            <tr>
                <th>Threes</th>
                <td>Total 3's</td>
                <td>{{ onesToSixes[3] }}</td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
            </tr>
            <tr>
                <th>Fours</th>
                <td>Total 4's</td>
                <td>{{ onesToSixes[4] }}</td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
            </tr>
            <tr>
                <th>Fives</th>
                <td>Total 5's</td>
                <td>{{ onesToSixes[5] }}</td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
            </tr>
            <tr>
                <th>Sixes</th>
                <td>Total 6's</td>
                <td>{{ onesToSixes[6] }}</td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
            </tr>
        </tbody>
        <tfoot>
            <tr>
                <th colspan="2">Total Points</th>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
            </tr>
            <tr>
                <th>Extra Bonus</th>
                <td>35 Points</td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
            </tr>
            <tr>
                <th colspan="2">Total Part 1</th>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
            </tr>
        </tfoot>
    </table>

    <table>
        <thead>
            <tr>
                <th>Part 2</th>
                <td>Score</td>
                <td>Game 1</td>
                <td>Game 2</td>
                <td>Game 3</td>
                <td>Game 4</td>
                <td>Game 5</td>
                <td>Game 6</td>
            </tr>
        </thead>
        <tbody>
            <tr>
                <th>Three of a Kind</th>
                <td>Total Dice</td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
            </tr>
            <tr>
                <th>Four of a Kind</th>
                <td>Total Dice</td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
            </tr>
            <tr>
                <th>Full House</th>
                <td>25 Points</td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
            </tr>
            <tr>
                <th>Small Straight</th>
                <td>30 Points</td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
            </tr>
            <tr>
                <th>Large Straight</th>
                <td>40 Points</td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
            </tr>
            <tr>
                <th>Yahtzee</th>
                <td>50 Points</td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
            </tr>
            <tr>
                <th>Chance</th>
                <td>Total Dice</td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
            </tr>
        </tbody>
        <tfoot>
            <tr>
                <th colspan="2">Total Part 2</th>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
            </tr>
            <tr>
                <th colspan="2">Total Part 1</th>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
            </tr>
            <tr>
                <th colspan="2">Total Score</th>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
            </tr>
        </tfoot>
    </table>
</template>

<style scoped>
table {
    margin: 25px;
    border-collapse: separate;
    border: black 3px solid;
    border-radius: 10px;
    table-layout: fixed;
    width: 100%;
    height: fit-content;
}

thead {
    font-weight: bold;
}

tr {
    border-bottom: solid black 2px;
}

td, th {
    border-left:solid black 2px;
    border-bottom: solid black 2px;
    font-size: large;
    height: 25px;
    line-height: 0;
}

th {
    font-weight: bold;
    border-left: none;
}

tfoot tr:last-child td, tfoot tr:last-child th {
    border-bottom: none;
}
</style>
