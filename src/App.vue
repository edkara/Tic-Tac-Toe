
<script setup lang="ts">
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import Board from "./components/Board.vue";
</script>

<template>
  <div class="cont">
    <Board />
  </div>
</template>

<style>

body {
  background-color: #1E293B;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.cont {
  margin: 0 auto;
  max-width: 350px;
  position: relative;
}

.board {
  height: 30rem;
  width: 30rem;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, 20%);
}

.row {
  height: 100%;
}

</style>
