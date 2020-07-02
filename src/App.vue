<template>
  <div id="app" @dragover.prevent @drop.prevent>
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <h2>Color Theme Generator</h2>
    <Dropzone msg="Welcome to Your Vue.js App" @dropzoneEmit="onDropzoneEmit" />
    <Palette @paletteEmit="onPaletteEmit" :palette="palette" />
    <div class="CodeColorsContainer">
      <CodeColors
        v-for="(value, name, index) in hljsClasses"
        :key="index"
        :name="name"
        :backgroundInput="value"
        @CodeColorEmit="onCodeColorEmit"
      >
      </CodeColors>
    </div>
    <CodeBlock />
    <button v-on:click="doThing">jkjk</button>
  </div>
</template>

<script>
import Dropzone from "@/components/Dropzone.vue"
import Palette from "@/components/Palette.vue"
import CodeColors from "@/components/CodeColors.vue"
import CodeBlock from "@/components/CodeBlock.vue"

export default {
  name: "App",
  components: {
    Dropzone,
    Palette,
    CodeColors,
    CodeBlock,
  },
  data: function() {
    return {
      palette: [],
      hljsClasses: {
        "background": "#aaaaaa",
        "color": "#aaaaaa",
        "comment": "#aaaaaa",
        "keyword": "#dd4400",
        "title": "#aaaaaa",
        "params": "#aaaaaa",
        "built-in": "#aaaaaa",
        "number": "#aaaaaa",
        "string": "#aaaaaa",
        "subst": "#aaaaaa",
        "regexp": "#aaaaaa",
      },
    }
  },
  computed: {},
  methods: {
    onDropzoneEmit(value) {
      this.palette = value.map(e => this.intArrayToHex(e))
    },
    onPaletteEmit(el) {
      this.$set(this.palette, el.id, el.value)
    },
    onCodeColorEmit(emit) {
      this.$set(this.hljsClasses, emit.name, emit.newValue)
    },
    intArrayToHex(array) {
      return "#" + array[0].toString(16) + array[1].toString(16) + array[2].toString(16)
    },
    doThing() {
      let keys = Object.keys(this.hljsClasses)
      keys.forEach((key) => {
        if (key === 'background' || key === "color"){
          let keyword = document.querySelectorAll(".hljs")
          keyword.forEach(el => {
            el.style.color = this.hljsClasses['color']
            el.style.background = this.hljsClasses['background']
          })
          
        }
        else{
          let query = ".hljs-" + key 
          let keyword = document.querySelectorAll(query)
          keyword.forEach(el => {
            el.style.color = this.hljsClasses[key]
          })

        // console.log(key, this.hljsClasses[key] )

        }
      })
    },
  },

  watch: {
    palette: function() {
      //newValue) {
      // console.log(this.palette, newValue)
    },
    hljsClasses: {
      handler: function () {
        this.doThing()
      },
      deep: true
    },
  },
  created() {},
}
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

h2 {
  text-shadow: 2px 2px aquamarine;
}
.highlight-container {
  width: 80%;
  text-align: left;
}
.hljs-keyword {
  color: green;
}
.palette-home {
  width: 100px;
  height: 100px;
  border: 1px solid;
}
.CodeColorsContainer {
  display: flex;
  flex-direction: row;
}
</style>
