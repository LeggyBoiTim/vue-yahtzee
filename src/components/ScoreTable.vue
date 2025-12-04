<script setup>
import { computed } from 'vue';

const dice = defineModel();

const diceCount = computed(() => {
    let count = {1: 0, 2: 0, 3: 0, 4: 0, 5: 0, 6: 0};
    for (let die of dice.value) {
        count[die]++;
    }
    return count;
});

const diceTotal = computed(() => {
    let sum = (total, num) => {return total + num};
    return dice.value.reduce(sum, 0);
});

const onesToSixes = computed(() => {
    let object = {};
    for (let face in diceCount.value) {
        object[face] = face * diceCount.value[face];
    }
    return object;
});

const findXOfAKind = (x, useEqual) => {
    for (let face in diceCount.value) {
        if ((useEqual && diceCount.value[face] === x) || (!useEqual && diceCount.value[face] >= x)) {
            return true;
        }
    }
    return false;
}

const threeOfAKind = computed(() => {
    return findXOfAKind(3, false) ? diceTotal.value : 0;
});

const fourOfAKind = computed(() => {
    return findXOfAKind(4, false) ? diceTotal.value : 0;
});

const fullHouse = computed(() => {
    return findXOfAKind(2, true) && findXOfAKind(3, true) ? 25 : 0;
});

const findSequentialDice = (x) => {
    let run = 0;
    for (let i in diceCount.value) {
        diceCount.value[i] > 0 ? run++ : run = 0;
        if (run === x) return true;
    }
    return false;
}

const smallStraight = computed(() => {
    return findSequentialDice(4) ? 30 : 0;
});

const largeStraight = computed(() => {
    return findSequentialDice(5) ? 40 : 0;
});

const yahtzee = computed(() => {
    return findXOfAKind(5, false) ? 50 : 0;
});

const totalPart1 = computed(() => {
    return diceTotal.value;
});

const extraBonus = computed(() => {
    return diceTotal.value >= 63 ? 35 : 0;
});

const totalPart1WithBonus = computed(() => {
    return diceTotal.value + extraBonus.value;
});

const totalPart2 = computed(() => {
    return threeOfAKind.value +
    fourOfAKind.value +
    fullHouse.value +
    smallStraight.value +
    largeStraight.value +
    yahtzee.value +
    totalPart1.value;
});

const grandTotal = computed(() => {
    return totalPart1WithBonus.value + totalPart2.value;
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
                <td>{{ onesToSixes[1] || '' }}</td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
            </tr>
            <tr>
                <th>Twos</th>
                <td>Total 2's</td>
                <td>{{ onesToSixes[2] || '' }}</td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
            </tr>
            <tr>
                <th>Threes</th>
                <td>Total 3's</td>
                <td>{{ onesToSixes[3] || '' }}</td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
            </tr>
            <tr>
                <th>Fours</th>
                <td>Total 4's</td>
                <td>{{ onesToSixes[4] || '' }}</td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
            </tr>
            <tr>
                <th>Fives</th>
                <td>Total 5's</td>
                <td>{{ onesToSixes[5] || '' }}</td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
            </tr>
            <tr>
                <th>Sixes</th>
                <td>Total 6's</td>
                <td>{{ onesToSixes[6] || '' }}</td>
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
                <td>{{ totalPart1 || '' }}</td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
            </tr>
            <tr>
                <th>Extra Bonus</th>
                <td>35 Points</td>
                <td>{{ extraBonus || '' }}</td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
            </tr>
            <tr>
                <th colspan="2">Total Part 1</th>
                <td>{{ totalPart1WithBonus || '' }}</td>
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
                <td>{{ threeOfAKind || '' }}</td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
            </tr>
            <tr>
                <th>Four of a Kind</th>
                <td>Total Dice</td>
                <td>{{ fourOfAKind || '' }}</td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
            </tr>
            <tr>
                <th>Full House</th>
                <td>25 Points</td>
                <td>{{ fullHouse || '' }}</td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
            </tr>
            <tr>
                <th>Small Straight</th>
                <td>30 Points</td>
                <td>{{ smallStraight || '' }}</td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
            </tr>
            <tr>
                <th>Large Straight</th>
                <td>40 Points</td>
                <td>{{ largeStraight || '' }}</td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
            </tr>
            <tr>
                <th>Yahtzee</th>
                <td>50 Points</td>
                <td>{{ yahtzee || '' }}</td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
            </tr>
            <tr>
                <th>Chance</th>
                <td>Total Dice</td>
                <td>{{ totalPart1 || '' }}</td>
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
                <td>{{ totalPart2 || '' }}</td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
            </tr>
            <tr>
                <th colspan="2">Total Part 1</th>
                <td>{{ totalPart1 || '' }}</td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
            </tr>
            <tr>
                <th colspan="2">Total Score</th>
                <td>{{ grandTotal || '' }}</td>
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
