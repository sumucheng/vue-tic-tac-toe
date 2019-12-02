<template>
  <div id="app">
    <div v-if="winner" class="over">{{winner}} win !</div>
    <div v-if="over" class="over">Game Over</div>
    <div class="wrapper">
      <div class="row">
        <Cell @click="click([0,0],$event)" :n="n" />
        <Cell @click="click([0,1],$event)" :n="n" />
        <Cell @click="click([0,2],$event)" :n="n" />
      </div>
      <div class="row">
        <Cell @click="click([1,0],$event)" :n="n" />
        <Cell @click="click([1,1],$event)" :n="n" />
        <Cell @click="click([1,2],$event)" :n="n" />
      </div>
      <div class="row">
        <Cell @click="click([2,0],$event)" :n="n" />
        <Cell @click="click([2,1],$event)" :n="n" />
        <Cell @click="click([2,2],$event)" :n="n" />
      </div>
      <div class="info">
        Next：
        <span class="next">{{n%2===0?'x':'o'}}</span>
      </div>
    </div>
  </div>
</template>

<script>
import Cell from "./Cell";

export default {
  name: "app",
  components: {
    Cell
  },
  data() {
    return {
      n: 0,
      winner: "",
      over: false,
      map: [["", "", ""], ["", "", ""], ["", "", ""]]
    };
  },
  methods: {
    click([i, j], text) {
      this.n += 1;
      this.map[i][j] = text;
      this.judge();
    },

    judge() {
      const map = this.map;
      for (let i = 0; i < 3; i++) {
        if (map[i][0] && map[i][0] === map[i][1] && map[i][1] === map[i][2]) {
          this.winner = map[i][0];
        }
      }
      for (let i = 0; i < 3; i++) {
        if (map[0][i] && map[0][i] === map[1][i] && map[1][i] === map[2][i]) {
          this.winner = map[0][i];
        }
      }
      if (map[0][0] && map[0][0] === map[1][1] && map[1][1] === map[2][2]) {
        this.winner = map[0][0];
      }
      if (map[2][0] && map[2][0] === map[1][1] && map[1][1] === map[0][2]) {
        this.winner = map[2][0];
      }
      if (this.n === 9 && !this.winner) {
        this.over = true;
      }
    }
  }
};
</script>

<style>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

#app {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 60vh;
}
.row {
  display: flex;
}
.wrapper {
  position: relative;
}
.info {
  font-size: 20px;
  width: 100px;
  left: 250px;
  top: 0;
  position: absolute;
}
.next {
  font-weight: 700;
  font-size: 32px;
}
.over {
  width: 100vw;
  height: 100vh;
  background: rgba(0, 0, 0, 0.5);
  position: fixed;
  top: 0;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  color: #fff;
  font-size: 80px;
  z-index: 3;
}
</style>
