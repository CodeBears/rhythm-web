<template>
  <div id="nav">
    <a
      href="https://www.linkedin.com/in/johnny-chen-6a4094188/"
      style="vertical-align: middle"
      target="_blank"
    >
      github</a
    >|
    <a href="https://github.com/CodeBears" style="vertical-align: middle" target="_blank"
      >linkedin</a
    >
  </div>
  <Board />
</template>

<script>
import Board from './components/Board.vue';

const githubSVG = require('@/assets/github.svg');

export default {
  name: 'App',
  components: {
    Board,
  },
  data() {
    return {
      githubSVG,
    };
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#nav {
  padding: 10px;
  display: flex;
  justify-content: flex-end;

  a {
    &:hover {
      color: darken(#eee, 10%);
    }
    font-weight: bold;
    color: #eee;
  }
}
</style>
