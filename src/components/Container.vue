<template>
  <section class="row" >
    <button @click="addWater(state.id)">🚰</button>
    <div v-bind:style="'margin-top:' + state.offset + 'px'">
      <div class="container">
        <div class="liquid" v-bind:style="'height:' + state.water + '%'"></div>
      </div>
    </div>
  </section>
</template>

<script>
import Vue from 'vue';
import Component from 'vue-class-component';

@Component({
  props: {
    addWater: Function,
    state: Object,
  },
})
export default class Container extends Vue {
}
</script>

<style>
  .container {
    display: flex;
    flex-direction: column-reverse;
    width: 40px;
    height: 100px;
    background-color: #eee;
    margin-top: 20px;
    transition: width 500ms;
  }

  .liquid {
    display: flex;
    flex-direction: column-reverse;
    width: 40px;
    height: 100px;
    background-color: blue;
    transition: height 500ms;
  }
</style>
