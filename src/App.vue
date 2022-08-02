<template>
  <h1>Rock - Paper - Scissors</h1>
  <GameStageRPS />
</template>

<script>
import GameStageRPS from "./components/GameStageRPS.vue";

export default {
  name: "App",
  components: {
    GameStageRPS,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
