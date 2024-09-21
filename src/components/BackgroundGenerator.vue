<template>
  <div>
    <div class="buttons-wrapper">
      <button @click="generatePattern">Generate pattern</button>
      <button @click="downloadImage">Download this image</button>
    </div>
    <canvas ref="canvas" :width="width" :height="height" style="border: 1px solid black;"></canvas>
  </div>
</template>

<script>
export default {
  props: {
    selectedColors: {
      type: Array,
      required: true
    },
  },
  data() {
    return {

      width: window.innerWidth * 0.9,
      height: window.innerHeight * 0.7
    };
  },
  methods: {
    generatePattern() {
      const canvas = this.$refs.canvas;
      const ctx = canvas.getContext('2d');

      ctx.clearRect(0, 0, this.width, this.height);

      const gradient = ctx.createLinearGradient(0, 0, this.width, this.height);
      this.selectedColors.forEach((color, index) => {
        gradient.addColorStop(index / (this.selectedColors.length - 1), color);
      });

      ctx.fillStyle = gradient;
      ctx.fillRect(0, 0, this.width, this.height);

      //snowflakes generate
      for (let i = 0; i < 100; i++) { // number of snowflakes
        const x = Math.random() * this.width;
        const y = Math.random() * this.height;
        const size = Math.random() * 10 + 5; // size of snowflakes 

        ctx.fillStyle = `rgba(255, 255, 255, ${Math.random() * 0.5 + 0.2})`;

        //draw snowflakes
        ctx.beginPath();
        this.drawSnowflake(ctx, x, y, size);
        ctx.fill();
      }
    },
    drawSnowflake(ctx, x, y, size) {
      const arms = 6; // snowflakes arms number
      for (let i = 0; i < arms; i++) {
        ctx.save();
        ctx.translate(x, y);
        ctx.rotate((Math.PI * 2 / arms) * i);
        ctx.moveTo(0, 0);
        ctx.lineTo(0, -size);
        ctx.lineTo(size / 4, -size / 2);
        ctx.lineTo(0, -size * 0.75);
        ctx.lineTo(-size / 4, -size / 2);
        ctx.lineTo(0, -size);
        ctx.strokeStyle = ctx.fillStyle;
        ctx.stroke();
        ctx.restore();
      }
    },
    downloadImage() {
      const canvas = this.$refs.canvas;
      const link = document.createElement('a');
      link.href = canvas.toDataURL('image/png');
      link.download = 'generated-background.png';
      link.click();
    }
  },
};
</script>

<style scoped>
canvas {
  margin-top: 20px;
}

.buttons-wrapper {
  width: 280px;
  display: flex;
  justify-content: space-between;
  margin: 0 auto;
}

button {
  padding: 10px 7px;
  border-radius: 8px;
  border: none;
  transition: 0.5s;
}

button:hover {
  background-color: #f9b282;
}

button:hover,
input[type="color"]:hover {
  cursor: pointer;
}
</style>