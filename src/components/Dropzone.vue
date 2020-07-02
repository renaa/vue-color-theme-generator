<template>
  <div
    class="dropzone"
    @drop="drop"
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
      palette: null,
    };
  },
  methods: {
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
          const colorThief = new ColorThief();
          const palette = colorThief.getPalette(self.image, 50, 9);
          self.$emit("dropzoneEmit", palette);
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
  display: flex;
  flex-direction: column;
  width: 100%;
  height: $size;
  background-color: aquamarine;
}
p {
  margin: auto;
}
img {
  width: 50%;
}
canvas {
  display: none;
}
</style>
