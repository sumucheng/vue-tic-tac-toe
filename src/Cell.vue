<template>
  <div class="cell" v-on:click="click">
    <template v-if="text">{{text}}</template>
    <template v-else></template>
  </div>
</template>

<script>
export default {
  props: ["n"],
  data() {
    return {
      text: ""
    };
  },

  methods: {
    click() {
      if (this.text) return;
      this.text = this.n % 2 === 0 ? "x" : "o";
      this.$emit("click", this.text);
    }
  }
};
</script>

<style>
.cell {
  border: 1px solid #999;
  width: 70px;
  height: 70px;
  font-size: 60px;
  text-align: center;
  font-weight: 600;
  line-height: 58px;
}
</style>
