<template>
  <div
    class="dropzone"
    @drop="drop"
    @dragover="allowDrop"
    @dragenter="dragEnter"
    @dragleave="dragLeave"
  >
    <p v-if="!imageLoaded">{{message}}</p>
    <div v-else>
    <img :src="src" ref="imgRef" />
    <canvas ref="canRef"></canvas>
    </div>
  </div>
</template>


<script>
export default {
  name: "Dropzone",
  props: {
    msg: String
  },
  data: function() {
    return {
      canvas: null,
      ctx: null,
      file: null,
      fileName: '',
      image: null,
      imageData: null,
      imageLoaded: false,
      message: "drop image here",
      src: "",
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
        this.loadPicture(file);
        this.imageLoaded = true;
      } else {
        this.message = "that was not an image file";
      }
    },
    loadPicture(file) {
      let self = this;
      var reader = new FileReader();
      reader.onload = function(e) {
        self.src = e.target.result;
        self.image = self.$refs.imgRef
        self.canvas = self.$refs.canRef
        self.ctx = self.canvas.getContext("2d");
        self.image.onload = function() {
          self.ctx.drawImage(self.image, 0, 0);
          self.imageData = self.ctx.getImageData(0,0, self.image.width, self.image.height)
        }
      };
      reader.readAsDataURL(file);
    }
  }
};
</script>


<style scoped lang="scss">
$size: 400px;

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
canvas{
  display: none;
}
</style>
