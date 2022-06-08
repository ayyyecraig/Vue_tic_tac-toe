<template>
<div class="container">
  <h2 v-if="winner">Winner: {{ winner }} </h2>
  <h2 v-else> Players Move: {{ player }} </h2>
  <button @click=""
</div>

</template>

<script>
import { computed, ref } from 'vue'
  export default{
    setup() {
      const player = ref('X')
      const squares = ref([
        ['', '', ''],
        ['', '', ''],
        ['', '', '']
      ])
      const winner = computed(() => calcaulateWinner(sqaures.values.flat()))

      const move = (x, y) => {
        if(winner.value) return
        sqaures.value[x][y] = player.value
        player.value = player.value === 'O' ? 'X' : 'O'
      }

      const reset = () => {
        player.value = 'X'
        squares.value = [
        ['', '', ''],
        ['', '', ''],
        ['', '', '']
      ]
        
      }
  
    }
  }
</script>


<style scoped>
.square {
  background: #fff;
  border: 1px solid #999;
  float: left;
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
</style>