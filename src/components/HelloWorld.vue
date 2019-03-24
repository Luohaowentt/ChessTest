<template>
  <div>
    <h1>贴贴五子棋</h1><br>
    <h3>回合数：{{turn}}&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{{player}}方的回合</h3>
    <br>
    <div class="chessboard">
      <div v-for="boxY in 14" :key="boxY">
        <div :class="getChessBoxClass(boxX,boxY)" :id="getChessBoxId(boxX,boxY)" v-for="boxX in 14" :key="boxX" >
          <div v-bind:class="{'chess-non':chessState[boxY-1][boxX-1]===0,'chess-black':chessState[boxY-1][boxX-1]===1,'chess-white':chessState[boxY-1][boxX-1]===2,}" :id="boxY+'-'+boxX" @click="play()"></div>
        </div><br>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      turn: 1,
      player: '白',
      player_sign: true,
      chessState: [[0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0], [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]]
    }
  },
  methods: {
    getChessBoxId: function (i, j) {
      return 'box_' + j + '_' + i
    },
    getChessBoxClass: function (i, j) {
      if ((i + j) % 2 === 1) { return 'chessBox_1' } else { return 'chessBox_2' }
    },
    play: function () {
      var el = event.currentTarget
      var coordinates = el.id.split('-')
      var y = coordinates[0] - 1
      var x = coordinates[1] - 1
      if (!this.chessState[y][x]) {
        this.turn++
        this.player_sign = !this.player_sign
        if (this.player_sign) {
          this.chessState[y][x] = 1
          this.player = '白'
        } else {
          this.chessState[y][x] = 2
          this.player = '黑'
        }
        // 判断胜利
        console.log('x--' + x + ',y--' + y)
        var winnerState = this.chessState[y][x] // 记录选手颜色
        var winConst = 1 // 记录连着棋子个数 本身算一个
        var winFlag = false
        // 横向做判断
        if (!winFlag) {
          winConst = 1
          for (var i = 1; i < 5; i++) { // 向左
            if (x - i < 0) {
              break
            }
            if (this.chessState[y][x - i] === winnerState) {
              winConst++
            } else {
              break
            }
          }
          for (i = 1; i < 5; i++) { // 向右
            if (x + i > 13) {
              break
            }
            if (this.chessState[y][x + i] === winnerState) {
              winConst++
            } else {
              break
            }
          }
          if (winConst >= 5) {
            winFlag = true
          }
        }
        // 纵向
        if (!winFlag) {
          winConst = 1
          for (i = 1; i < 5; i++) { // 向上
            if (y - i < 0) {
              break
            }
            if (this.chessState[y - i][x] === winnerState) {
              winConst++
            } else {
              break
            }
          }
          for (i = 1; i < 5; i++) { // 向右
            if (y + i > 13) {
              break
            }
            if (this.chessState[y + i][x] === winnerState) {
              winConst++
            } else {
              break
            }
          }
          if (winConst >= 5) {
            winFlag = true
          }
        }
        // 左下到右上
        if (!winFlag) {
          winConst = 1
          for (i = 1; i < 5; i++) { // 向左下
            if (y + i > 13 || x - i < 0) {
              break
            }
            if (this.chessState[y + i][x - i] === winnerState) {
              winConst++
            } else {
              break
            }
          }
          for (i = 1; i < 5; i++) { // 向右上
            if (y - i < 0 || x + i > 13) {
              break
            }
            if (this.chessState[y - i][x + i] === winnerState) {
              winConst++
            } else {
              break
            }
          }
          if (winConst >= 5) {
            winFlag = true
          }
        }
        // 左上到右下
        if (!winFlag) {
          winConst = 1
          for (i = 1; i < 5; i++) { // 向右下
            if (y + i > 13 || x + i > 13) {
              break
            }
            if (this.chessState[y + i][x + i] === winnerState) {
              winConst++
            } else {
              break
            }
          }
          for (i = 1; i < 5; i++) { // 向左上
            if (y - i < 0 || x - i < 0) {
              break
            }
            if (this.chessState[y - i][x - i] === winnerState) {
              winConst++
            } else {
              break
            }
          }
          if (winConst >= 5) {
            winFlag = true
          }
        }
        if (winFlag) {
          if (this.player_sign === true) {
            this.$alert('黑方获胜', '游戏结束', {
              confirmButtonText: '确定'
            })
          } else {
            this.$alert('白方获胜', '游戏结束', {
              confirmButtonText: '确定'
            })
          }
        }
      } else {
        this.$message({
          message: '这里已经有棋子了哦！',
          type: 'warning'
        })
      }
      // console.log(x + '-' + y)
    },
    clearBoard: function () {
      for (var i = 0; i < 14; i++) {
        for (var j = 0; j < 14; j++) {
          this.chessState[i][j] = 0
        }
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  @import "../assets/css/public.css";
  @import "../assets/css/chessStyle.css";
</style>
