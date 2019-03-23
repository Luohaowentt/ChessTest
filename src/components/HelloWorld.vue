<template>
  <div>
    <h1>贴贴五子棋</h1><br>
    <div class="chessboard">
      <div v-for="boxY in 14" :key="boxY">
        <div class="chessBox" :id="getChessBoxId(boxX,boxY)" v-for="boxX in 14" :key="boxX" @click="play">{{boxY}}-{{boxX}}</div><br>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
    }
  },
  methods: {
    getChessBoxId: function (i, j) {
      return 'box_' + j + '_' + i
    },
    play: function () {
      var el = event.currentTarget
      console.log(el.id)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  @import "../assets/css/public.css";
  @import "../assets/css/chessStyle.css";
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
