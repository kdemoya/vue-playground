<template>
  <div>
    <section class="left">
      <button @click="changeCamera(containers.first.id)">Cam 1</button>
      <button @click="changeCamera(containers.second.id)">Cam 2</button>
      <button @click="changeCamera('main')">Reset Camera</button>
    </section>
    <section v-show="isMainCamera() || camera.includes(containers.first.id)" class="row">
      <Container :state="containers.first" v-bind="{addWater}" />
    </section>
    <section class="row">
      <Link />
    </section>
    <section v-show="isMainCamera() || camera.includes(containers.second.id)" class="row">
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
const MAIN_CAMERA_ID = 'main';

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

  camera = MAIN_CAMERA_ID;

  changeCamera(id) {
    this.camera = id;
  }

  isMainCamera() {
    return this.camera === MAIN_CAMERA_ID;
  }

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
  .left {
    text-align: left;
    margin-bottom: 20px;
  }
</style>
