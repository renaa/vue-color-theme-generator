<template>
  <div id="app" @dragover="allowDrop">
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <Dropzone msg="Welcome to Your Vue.js App" />
    <form >
          </form>
  </div>
</template>

<script>
import Dropzone from "./components/Dropzone.vue";

export default {
  name: "App",
  components: {
    Dropzone
  },
  methods: {
    allowDrop: function(event) {
      event.preventDefault();
    },
  }
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
