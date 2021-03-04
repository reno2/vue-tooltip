<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js App" />
    <VTooltip>
      <div class="example_text">
        Lorem ipsum dolor sit amet, consectetur adipiscing elit.
      </div>
    </VTooltip>
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import VTooltip from "./components/Tooltip.vue";

export default {
  name: "App",
  components: {
    HelloWorld,
    VTooltip,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  width: 1170px;
  margin: 20px auto;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
