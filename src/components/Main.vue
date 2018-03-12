<template>
  <div>
    <section class="row">
      <Container :state="containers.first" v-bind="{addWater}" />
    </section>
    <section class="row">
      <Link />
    </section>
    <section class="row">
      <Container :state="containers.second" v-bind="{addWater}" />
    </section>
  </div>
</template>

<script>
import Vue from 'vue';
import Component from 'vue-class-component';
import Container from './Container';
import Link from './Link';

const OFFSET = 40;
const ADD_QTY = 10;
const FIRST_CONTAINER_ID = 'first';
const SECOND_CONTAINER_ID = 'second';

@Component({
  props: {},
  components: {
    Container,
    Link,
  },
})
export default class Main extends Vue {
  containers = {
    [FIRST_CONTAINER_ID]: { water: 10, id: FIRST_CONTAINER_ID, offset: 0 },
    [SECOND_CONTAINER_ID]: { water: 10, id: SECOND_CONTAINER_ID, offset: OFFSET },
  };

  setContainerWater(containerId, addition) {
    const newValue = this.containers[containerId].water + addition;
    this.containers[containerId].water = Math.min(100, Math.max(0, newValue));
  }

  addWater(containerId) {
    const shouldDistribute = this.containers[SECOND_CONTAINER_ID].water >= OFFSET;
    this.setContainerWater(containerId, ADD_QTY);

    if (containerId === FIRST_CONTAINER_ID || shouldDistribute) {
      setTimeout(() => {
        Object.keys(this.containers).forEach((key) => {
          this.setContainerWater(key, ADD_QTY / 2);
        });
      }, 200);
    }
  }
}
</script>

<style>
  .row {
    float: left;
  }
</style>
