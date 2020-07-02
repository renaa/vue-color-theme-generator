<template>
  <div class="palette-container" ref="draggableContainer" id="draggable-container">
    <input
      type="color"
      v-for="(item, index) in palette"
      :value="palette[index]"
      :key="index"
      :id="index"
      draggable="true"
      @change="log"
      @dragstart="dragStart"
      @dragover.stop

    />
  </div>
</template>


<script>
export default {
  name: "Palette",
  props: {
    palette: Array,
    
  },
  data: function() {
    return {
      
    };
  },
  methods: {
    log(e) {
      this.$emit("paletteEmit", e.target);
    },
    dragStart: e => {
      const target = e.target
      e.dataTransfer.setData('color_id', target.id)
    },
    
  }
};
</script>


<style scoped lang="scss">
$size: 100px;
input {
  height: $size;
  width: $size;
  margin: 0;
  margin: 1em;
  cursor: move;
}

input:hover {
  box-shadow: 0px 0px 4px 4px #aaa;
}
.palette-container {
  background-color: #efefef;
  padding: 1em;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: flex-start;

  padding: 0;
}
</style>
