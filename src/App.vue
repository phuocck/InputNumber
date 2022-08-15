<template>
  <HelloWorld msg="Welcome to Your Vue.js App" />

  <ms-number :label="'Số tiền'" v-model="amount" :initValue="amount"></ms-number>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import MsNumber from "./components/MsNumber.vue";
import {ref} from 'vue';

export default {
  name: "App",
  components: {
    HelloWorld,
    MsNumber,
  },
  setup(props, { emit }) {
    const amount = ref(1000);
    return { amount };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

/* eslint-disable */
