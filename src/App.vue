<template>
  <div class="wraper">
    <div class="chess">
      <div>第{{n}}手</div>
      <div class="row">
        <Cell @click="onClickCell(0,$event)" :n="n" ref="c1" />
        <Cell @click="onClickCell(1,$event)" :n="n" ref="c2" />
        <Cell @click="onClickCell(2,$event)" :n="n" ref="c3" />
      </div>
      <div class="row">
        <Cell @click="onClickCell(3,$event)" :n="n" ref="c4" />
        <Cell @click="onClickCell(4,$event)" :n="n" ref="c5" />
        <Cell @click="onClickCell(5,$event)" :n="n" ref="c6" />
      </div>
      <div class="row">
        <Cell @click="onClickCell(6,$event)" :n="n" ref="c7" />
        <Cell @click="onClickCell(7,$event)" :n="n" ref="c8" />
        <Cell @click="onClickCell(8,$event)" :n="n" ref="c9" />
      </div>
      <div>结果:{{result==null ?'胜负未分':`胜方为${result}`}}</div>
    </div>
  </div>
</template>

<script>
import Cell from "./Cell";

export default {
  //   name: 'App',
  data() {
    return {
      n: 0,
      map: [
        [null, null, null],
        [null, null, null],
        [null, null, null]
      ],
      result: null
    };
  },
  components: {
    Cell
  },
  methods: {
    onClickCell(i, text) {
      // console.log(`${i}号被点击,内容是:${text}`);
      this.map[Math.floor(i / 3)][i % 3] = text;
      this.n += 1;
      // console.log(this.result);
      this.tell();
    },
    tell() {
      const map = this.map;
      for (let i = 0; i < 2; i++) {
        if (
          map[i][0] != null &&
          map[i][0] == map[i][1] &&
          map[i][0] == map[i][2]
        ) {
          this.result = map[i][0];
          this.finish();
        }
      }
      for (let j = 0; j < 2; j++) {
        if (
          map[0][j] != null &&
          map[0][j] == map[1][j] &&
          map[0][j] == map[2][j]
        ) {
          this.result = map[0][j];
          this.finish();
        }
      }
      if (
        map[0][0] != null &&
        map[0][0] == map[1][1] &&
        map[0][0] == map[2][2]
      ) {
        this.result = map[0][0];
        this.finish();
      }
      if (
        map[0][2] != null &&
        map[0][2] == map[1][1] &&
        map[0][2] == map[2][0]
      ) {
        this.result = map[0][2];
        this.finish();
      }
    },
    finish() {
      const map = this.map;
      if (map[0][0] == null) {
        this.$refs.c1.text = " ";
      }
      if (map[0][1] == null) {
        this.$refs.c2.text = " ";
      }
      if (map[0][2] == null) {
        this.$refs.c3.text = " ";
      }
      if (map[1][0] == null) {
        this.$refs.c4.text = " ";
      }
      if (map[1][1] == null) {
        this.$refs.c5.text = " ";
      }
      if (map[1][2] == null) {
        this.$refs.c6.text = " ";
      }
      if (map[2][0] == null) {
        this.$refs.c7.text = " ";
      }
      if (map[2][1] == null) {
        this.$refs.c8.text = " ";
      }
      if (map[2][2] == null) {
        this.$refs.c9.text = " ";
      }
    }
  }
};
</script>

<style>
.row {
  display: flex;
}
.chess{
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
</style>
