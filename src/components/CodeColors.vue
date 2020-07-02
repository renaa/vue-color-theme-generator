<template>
  <div id="CodeColors" class="CodeColors" :style='{background: background, color: color}' @dragover.prevent @drop.prevent="drop">
    {{ name }}
  </div>
</template>

<script>
export default {
  props: [
    'name',
    'backgroundInput',
  ],
  data: function(){
    return{
      color: '#000000',
      background: this.backgroundInput
    }

  },
  methods: {
    drop: function (e) {
      const color_id = e.dataTransfer.getData("color_id")
      const input = document.getElementById(color_id)
      this.background = input.value
    },
    makeTextReadable: () => {},
  },
  watch: {
    background: function(newValue){
      let r = parseInt(newValue.substr(1, 2), 16)
      let g = parseInt(newValue.substr(3, 2), 16)
      let b = parseInt(newValue.substr(5, 2), 16)
      let threshold = 166
      //https://stackoverflow.com/questions/3942878/how-to-decide-font-color-in-white-or-black-depending-on-background-color
      if (r*0.299 + g*0.587 + b*0.114 > threshold){
        this.color = "#111"
      }
      else{
        this.color = "#eee"
      }
      this.$emit('CodeColorEmit', {newValue: newValue, name: this.name})
    }
  }
}
</script>

<style lang="scss" scoped>
#CodeColors {
  width: 100px;
  height: 100px;
  border: 1px solid;
  display: flex;
  justify-content: center;
  align-items: center;
}
div{
  margin:0 auto;
}
</style>
