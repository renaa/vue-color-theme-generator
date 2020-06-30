<template>
  <div
    class="dropzone"
    @drop="drop"
    @dragover="allowDrop"
    @dragenter="dragEnter"
    @dragleave="dragLeave"
  >
    <p @dragenter="dragEnter" v-if="!imageLoaded">{{message}}</p>
    <div v-else>
      <img :src="src" ref="imgRef" />
      <canvas ref="canRef"></canvas>
    </div>
  </div>
</template>


<script>
import ColorThief from "colorthief";

export default {
  name: "Dropzone",
  props: {
    msg: String
  },
  data: function() {
    return {
      file: null,
      fileName: "",
      image: null,
      imageLoaded: false,
      message: "drop image here",
      src: "",
      palette: null
    };
  },
  methods: {
    allowDrop: function(event) {
      event.preventDefault();
    },
    dragEnter: function() {
      this.message = '"feed me" - 🦁';
    },
    dragLeave: function() {
      this.message = "drop image here";
    },
    drop: function(event) {
      event.preventDefault();
      if (/image\/*/.test(event.dataTransfer.files[0].type)) {
        let file = event.dataTransfer.files[0];
        this.getPalette(file);
        this.imageLoaded = true;
      } else {
        this.message = "that was not an image file";
      }
    },
    getPalette(file) {
      let self = this;
      let reader = new FileReader();
      reader.onload = function(e) {
        self.src = e.target.result;
        self.image = self.$refs.imgRef;
        self.image.onload = function() {
          // let canvas = document.createElement("canvas");
          // let ctx = canvas.getContext("2d");
          // ctx.drawImage(img, 0, 0);
          // let imageData = ctx.getImageData(0, 0, img.width, img.height).data;
          let colorThief = new ColorThief();
          self.palette = colorThief.getPalette(self.image, 50, 9);
          self.$emit("paletteEmit", self.palette);
        };
      };
      reader.readAsDataURL(file);
    }
  }
};
</script>


<style scoped lang="scss">
$size: 400px;

* {
  font-family: Menlo, Consolas, "Courier New", monospace;
}
div {
  margin: auto;
  display: flex;
  flex-direction: column;
  width: $size;
  height: $size;
  background-color: aquamarine;
  * {
    margin: auto;
  }
}
img {
  width: 100%;
}
canvas {
  display: none;
}
</style>
