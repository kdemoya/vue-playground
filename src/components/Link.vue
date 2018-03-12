<template>
  <div class="channel">
    <div class="liquid" style="height: 5px;"></div>
  </div>
</template>

<script>
import Vue from 'vue';
import Component from 'vue-class-component';

@Component({
  props: {
    water: Number,
  },
})
export default class Link extends Vue {
}
</script>

<style>
  .channel {
    width: 40px;
    height: 5px;
    background-color: #eee;
    transition: width 500ms;
    margin-top: 138px;
  }
</style>
