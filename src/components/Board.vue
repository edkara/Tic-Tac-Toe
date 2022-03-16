<script setup lang="ts">
import { computed, reactive, ref, toRefs, Prop } from "vue";

const player = ref("X");

const gameBoard = ref([
  ["", "", ""],
  ["", "", ""],
  ["", "", ""],
]);

function calculateWinner(squares) {
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

  //   const winningMoves = reactive({
  //     moves: [] as any,
  //   });

  for (let i = 0; i < lines.length; i++) {
    const [a, b, c] = lines[i];
    if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
      //   winningMoves.moves.push(a);
      //   winningMoves.moves.push(b);
      //   winningMoves.moves.push(c);
      //   console.log(a);
      //   console.log(b);
      //   console.log(c);
      return squares[a];
    }
  }
  return null;
}

const winner = computed(() => calculateWinner(gameBoard.value.flat()));

function makeMove(x: number, y: number) {
  if (winner.value) return;

  if (gameBoard.value[x][y] !== "") return;

  gameBoard.value[x][y] = player.value;

  if (player.value === "X") {
    player.value = "O";
  } else {
    player.value = "X";
  }
}

function resetGame() {
  gameBoard.value = [
    ["", "", ""],
    ["", "", ""],
    ["", "", ""],
  ];
  player.value = "X";
}
</script>

<template>
  <div class="board grid gap-4 grid-rows-3 bg-sky-50 p-4">
    <div class="row grid grid-cols-3" v-for="(row, x) in gameBoard" :key="x">
      <div
        class="
          board__cell
          shadow
          hover:shadow-2xl
          p-2
          material-icons-outlined
          text-6xl
          cursor-pointer
          flex
          items-center
          justify-center
        "
        v-for="(col, y) in row"
        :key="y"
        @click="makeMove(x, y)"
      >
        {{ col === "X" ? "close" : col === "O" ? "circle" : "" }}
      </div>
    </div>
  </div>

  <h2 v-if="winner" class="text-6xl font-bold mb-8 text-white">
    Winner: Player {{ winner }}!
  </h2>

  <button
    v-if="winner"
    @click="resetGame"
    class="
      px-4
      py-2
      bg-pink-500
      rounded
      uppercase
      font-bold
      hover:bg-pink-600
      duration-300
    "
  >
    Reset Game!
  </button>
  <!-- 
  <h2
    v-for="(moves, index) in winningMoves"
    :key="index"
    class="text-6xl font-light mb-8 text-white"
  >
    {{ moves }}
  </h2> -->
</template>



<style scoped>
</style>