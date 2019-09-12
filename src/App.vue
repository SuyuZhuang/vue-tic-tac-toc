<template>
  <div class="wrapper">
    <div>第{{n}}手</div>
    <div class="chess">
      <div class="row">
        <Cell v-on:click="onClickCell(0,$event)" v-bind:n="n" :finished="finished" />
        <Cell v-on:click="onClickCell(1,$event)" :n="n" :finished="finished" />
        <Cell v-on:click="onClickCell(2,$event)" :n="n" :finished="finished" />
      </div>
      <div class="row">
        <Cell v-on:click="onClickCell(3,$event)" :n="n" :finished="finished" />
        <Cell v-on:click="onClickCell(4,$event)" :n="n" :finished="finished" />
        <Cell v-on:click="onClickCell(5,$event)" :n="n" :finished="finished" />
      </div>
      <div class="row">
        <Cell v-on:click="onClickCell(6,$event)" :n="n" :finished="finished" />
        <Cell v-on:click="onClickCell(7,$event)" :n="n" :finished="finished" />
        <Cell v-on:click="onClickCell(8,$event)" :n="n" :finished="finished" />
      </div>
    </div>
    <div>结果：{{result === null ? "胜负未分" : `胜方为${result}`}}</div>
  </div>
</template>

<script>
import Cell from "./Cell";
export default {
  components: { Cell },
  data() {
    return {
      n: 0,
      map: [[null, null, null], [null, null, null], [null, null, null]],
      result: null,
      finished: false
    };
  },
  methods: {
    onClickCell(i, text) {
      console.log(`${i}号Cell被点了,内容是${text}`);
      this.n++;
      this.map[Math.floor(i / 3)][i % 3] = text;
      this.tell();
    },
    tell() {
      for (let i = 0; i < 3; i++) {
        if (
          this.map[i][0] === this.map[i][1] &&
          this.map[i][1] === this.map[i][2] &&
          this.map[i][0] !== null
        ) {
          console.log("第" + i + "行全相等");
          this.result = this.map[i][0];
          this.finished = true;
        }

        if (
          this.map[0][i] === this.map[1][i] &&
          this.map[1][i] === this.map[2][i] &&
          this.map[0][i] !== null
        ) {
          console.log("第" + i + "列全相等");
          this.result = this.map[0][i];
          this.finished = true;
        }
      }
      if (
        this.map[0][0] === this.map[1][1] &&
        this.map[1][1] === this.map[2][2] &&
        this.map[1][1] !== null
      ) {
        console.log("右斜对角全等");
        this.result = this.map[0][0];
        this.finished = true;
      }

      if (
        this.map[0][2] === this.map[1][1] &&
        this.map[1][1] === this.map[2][0] &&
        this.map[1][1] !== null
      ) {
        console.log("左斜对角全等");
        this.result = this.map[0][2];
        this.finished = true;
      }
    }
  }
};
</script>

<style>
.row {
  display: flex;
}
.wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
</style>
