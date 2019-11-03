<template>
  <div id="app">
    <!-- Text Header -->
    <h2 id="game-header">Let's play the Game!</h2>

    <!-- Tic tac toe -->
    <tic-tac-toe />
  </div>
</template>

<script>
import TicTacToe from '@/components/tic-tac-toe';

export default {
  name: 'app',
  components: {
    TicTacToe
  }
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

#game-header {
  color: #08ee08;
  font-weight: 900;
}

body {
  background-color: #367588;
}
</style>
