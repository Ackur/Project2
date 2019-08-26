<template>
  <div class="progress">
    <div class="progress-bar" v-bind:style="width"></div>
  </div>
</template>

<script>
export default {
  props: {
    max: Number,
    val: Number
  },
  computed: {
    width() {
      let w = this.val / this.max * 100;
      if (w > 100) {
        w = 100;
      } else if (w < 0) {
        w = 0;
      }
      return {
        width: w + "%"
      };
    }
  }
};
</script>

<style>
</style>

  <!--  --App.vue-- -->
 <!-- <AppProgress
      v-bind:val="sum"
      v-bind:max="maxNumbers * 5"
    ></AppProgress>
    <h2 v-show="!itemActive">You Profit: {{sum}}</h2>
    <button
      class="btn btn-success"
      v-on:click="itemActive = !itemActive"
      v-bind:title="btnText"
    >{{btnText}}</button>
    <button
      class="btn btn-info"
      v-bind:disabled="done"
      v-on:click="addNumber"
      v-on:contextmenu.prevent="numbers.pop()"
    >push/pop</button>
    <AppProgress
      v-bind:max="maxNumbers"
      v-bind:val="numbers.length"
    ></AppProgress>
    <p v-for="(number, i) in numbers" v-bind:index="++i" v-bind:key="number.id">{{i}}: {{number}}</p> -->