<template>
  <div class="container">
    <h2 v-if="winner">Winner: {{ winner }}</h2>
    <h2 v-else>Players Move: {{ player }}</h2>
    <button @click="reset" class="btn">Press here to reset</button>
    <div v-for="x in 3" :key="x" class="row">
      <button v-for="y in 3" :key="y" class="square" @click="move(x, y)">
        {{ squares[x][y] }}
      </button>
    </div>
 
  </div>
</template>

<script>
import { computed, onMounted, ref, watch } from "vue";

const calcaulateWinner = (squares) => {
  const lines = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6],
  ];
  for (let i = 0; i < lines.length; i++) {
    const [a, b, c] = lines[i];
    if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
      return `${squares[a]}Wins!`;
    } else {
      return null;
    }
  }
};
export default {
  setup() {
    const player = ref("X");
    const squares = ref([
      ["", "", "", ""],
      ["", "", "", ""],
      ["", "", "", ""],
      ["", "", "", ""],
    ]);
    const winner = computed(() => calcaulateWinner(squares.value));

    const move = (x, y) => {
      if (winner.value) return;
      squares.value[x][y] = player.value;
      player.value = player.value === "O" ? "X" : "O";
    };

    const reset = () => {
      player.value = "X";
      squares.value = [
        ["", "", "", ""],
        ["", "", "", ""],
        ["", "", "", ""],
        ["", "", "", ""],
      ];
    };
    const history = ref([]);
    watch(winner, (current, previous) => {
      if (current && !previous) {
        history.value.push(current);
        localStorage.setItem("history", JSON.stringify(history.value));
      }
    });

    onMounted(() => {
      history.value = JSON.parse(localStorage.getItem("history")) ?? [];
    });
    return { winner, player, squares, move, reset, history };
  },
};
</script>

<style scoped>


.square {
 background-image: linear-gradient(280deg, #96e2c6, rgba(206, 146, 179, 0.651));  
   border-right: #cf6d6d solid 9px;
    border-bottom: #5a2828 solid 8px;
    border-left: #cb9797 solid 11px;
    border-top: #e7bbbb solid 9px;
  float: center;
  font-size: 70px;
  font-weight: bold;
  line-height: 34px;
  height: 100px;
  margin-right: -1px;
  margin-top: -1px;
  padding: 0;
  text-align: center;
  width: 100px;

}

.btn{
    width: 408px;
    height: 68px;
  
    color: black;
    background-color: #edc2c2;
    font-family: 'Shizuru';
    font-size: 30px;
    margin-inline: 549px;
    border-right: #cf6d6d solid 9px;
    border-bottom: #5a2828 solid 8px;
    border-left: #cb9797 solid 11px;
    border-top: #e7bbbb solid 9px;

}
</style>
