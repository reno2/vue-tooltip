<template>
  <div class="hello">
    <h1>{{ msg }}</h1>

    <ul>
      <li>
        <a href="https://router.vuejs.org" target="_blank" rel="noopener"
          >vue-router</a
        >
      </li>
      <li>
        <a href="https://vuex.vuejs.org" target="_blank" rel="noopener">vuex</a>
      </li>
      <li>
        <a
          href="https://github.com/vuejs/vue-devtools#vue-devtools"
          target="_blank"
          rel="noopener"
          >vue-devtools</a
        >
      </li>
      <li>
        <VTooltip>
          <template v-slot:target>
            <a
              href="https://vue-loader.vuejs.org"
              target="_blank"
              rel="noopener"
              >Tooltip</a
            >
          </template>
          <div class="example_text">
            Lorem ipsum dolor sit amet, consectetur adipiscing elit.
          </div>
        </VTooltip>
      </li>
      <li>
        <a
          href="https://github.com/vuejs/awesome-vue"
          target="_blank"
          rel="noopener"
          >awesome-vue</a
        >
      </li>
    </ul>
  </div>
</template>

<script>
import VTooltip from "../components/Tooltip.vue";
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  components: {
    VTooltip,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
