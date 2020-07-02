<template>
  <div id="app" @dragover.prevent @drop.prevent>
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <h2>Color Theme Generator</h2>
    <Dropzone msg="Welcome to Your Vue.js App" @dropzoneEmit="onDropzoneEmit" />
    <Palette @paletteEmit="onPaletteEmit"  :palette="palette"/>
    <div class='p'>{{palette}}</div>

    <form></form>
  </div>
</template>

<script>
import Dropzone from "@/components/Dropzone.vue";
import Palette from "@/components/Palette.vue";

export default {
  name: "App",
  components: {
    Dropzone,
    Palette
  },
  data: function() {
    return {
      palette: []
    };
  },
  computed: {
  },
  methods: {
    onDropzoneEmit(value) {
      this.palette = value.map(e => this.intArrayToHex(e));
    },
    onPaletteEmit(el) {
      this.$set(this.palette, el.id, el.value)
    },
    intArrayToHex(array) {
  return "#" + array[0].toString(16) + array[1].toString(16) + array[2].toString(16);
}  
  },
  watch: {
    palette: function(newValue) {
      console.log(this.palette, newValue)
    }
  }
};
</script>

<style lang="scss">
* {
  margin: auto;
}
* + * {
  margin-top: 1em;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.p{
  font-family: "Lucida Console", Monaco, monospace; 
}
h2{
  text-shadow: 2px 2px aquamarine;
  
}
</style>
