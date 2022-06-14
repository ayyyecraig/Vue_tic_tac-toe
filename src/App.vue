<template>

  <BoardGame />
</template>

<script>
import BoardGame from './components/BoardGame.vue'

export default {
  name: 'App',
  components: {
   BoardGame
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
    background-image: url(https://static.vecteezy.com/system/resources/previews/000/256/896/original/abstract-marble-texture-vector-design.jpg) ;
    background-repeat: repeat-x;
    background-size: 627px;
      font-family: 'Shizuru';
    font-size: 50px;
}
</style>
