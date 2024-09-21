<template>
  <div id="app">
    <h1>Background image generator</h1>
    <div class="pickers-wrapper">
      <ColorPicker label="Color 1" :modelValue="colors[0]" :colors="colors" @updateColors="updateColors" />
      <ColorPicker label="Color 2" :modelValue="colors[1]" :colors="colors" @updateColors="updateColors" />
      <ColorPicker label="Color 3" :modelValue="colors[2]" :colors="colors" @updateColors="updateColors" />
    </div>
    <BackgroundGenerator :selectedColors="colors" @updateState="updateState" />
  </div>
</template>

<script>
import BackgroundGenerator from './components/BackgroundGenerator.vue';
import ColorPicker from './components/ColorPicker.vue';

export default {
  components: {
    BackgroundGenerator,
    ColorPicker
  },
  data() {
    return {
      colors: ['#ff0000', '#00ff00', '#0000ff'],
      sharedState: 'Начальное состояние'
    };
  },
  methods: {
    updateColors(index, newColor) {
      this.colors[index] = newColor;
    },
    updateState(newState) {
      this.sharedState = newState;
    },
  }
};
</script>

<style>
body {
  margin: 0;
  padding: 0;
}

#app {
  margin: 0;
  padding: 0;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

h1 {
  font-family: monospace;
  color: #cb6f32;
}

.pickers-wrapper {
  width: 200px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
}
</style>
