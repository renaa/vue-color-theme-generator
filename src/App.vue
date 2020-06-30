<template>
  <div id="app" @dragover="allowDrop">
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <Dropzone msg="Welcome to Your Vue.js App" @paletteEmit="onChildEmit" />
    <div>{{x}}</div>
    <div>{{y}}</div>

    <form></form>
  </div>
</template>

<script>
import Dropzone from "@/components/Dropzone.vue";

export default {
  name: "App",
  components: {
    Dropzone
  },
  data: function() {
    return {
      palette: [],
      y: 0
    };
  },
  computed: {
    x: function() {
      return this.palette[0];
    }
  },
  methods: {
    allowDrop: function(event) {
      event.preventDefault();
    },
    onChildEmit(value) {
      this.palette = value;
    }
  },
  watch: {
    palette: function(newValue) {
      this.y = newValue[0];
    }
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
