<template>
  <div class="highlight-container">
      <pre v-highlightjs><code class="javascript">{{ sourcecode }}</code></pre>
    </div>
</template>

<script>
export default {
  props: [
    
  ],
  data: function(){
    return{
      sourcecode: `
      
hljs.initHighlightingOnLoad()
import "./styles.css";
// import {kMeansClustering} from './kmeans.js';
const numberOfColors = 35;
let fileName;
import ColorThief from '../node_modules/colorthief/dist/color-thief.mjs'

function resetColorsInside() {
  colors.innerHTML = "";
}
function initColor(color, i) {
  color.draggable = "true";
  color.type = "color";
  color.value = intArrayToHex(palette.values[i]);
 
  color.addEventListener("change", e => {
    let color = e.target;
    let colors = color.parentNode;
    let i = Array.prototype.indexOf.call(colors.children, color);
    let newColor = hexToIntArray(color.value);
    let newPalette = palette.values;
    newPalette[i] = newColor;
    palette.updateValue(newPalette);

  })

  function dropHandler(ev) {
  ev.preventDefault();
  if (ev.dataTransfer.files.length > 1) {
    // ("more than one file")
  }
  if (/image\\/*/.test(ev.dataTransfer.files[0].type)) {
    // ("first file is an image file")
    var file = ev.dataTransfer.files[0];
    fileName = file.name;
    var fr = new FileReader();
    fr.onload = () => insertImage(file, fr);
    fr.readAsDataURL(file);
  }
}

`
    }

  },
  
}
</script>

<style lang="scss" scoped>

</style>
