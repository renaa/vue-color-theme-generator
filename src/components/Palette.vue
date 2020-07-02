<template>
  <div class='palette-container'>
    <input v-for="(item, index) in palette" :key='index' :id='index' type="color" @change="log" :value="palette[index]" >
  </div>
</template>


<script>
export default {
  name: "Palette",
  props: {
    palette: Array
  },
  methods: {
    log(e){
      this.$emit('paletteEmit', e.target)
    }
  }
};
</script>


<style scoped lang="scss">
  $size:100px;
  input{
    height: $size;
    width: $size;
    margin: 0;
    margin: 1em;
  }

  input:hover {
  box-shadow: 0px 0px 4px 4px #aaa;
}
  .palette-container{
    background-color: #efefef;
    padding: 1em;
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: flex-start;

    padding: 0;
  }
</style>
