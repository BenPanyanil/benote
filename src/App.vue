<template>
  <div class="draggables-container">
    <div 
      ref="draggable" 
      @mousedown.prevent="dragElement" 
      class="card">
        Drag me cholo!
      </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      start_x: null,
      start_y: null,
      change_x: null,
      change_y: null,
      draggable: null,
    }
  },
  mounted() {
    this.draggable = this.$refs.draggable
  },
  methods: {
    dragElement(e) {
      // mouse cursor position at start
      this.start_x = e.clientX;
      this.start_y = e.clientY;

      document.onmouseup = this.stopDrag;
      document.onmousemove = this.moveCard;
    },
    moveCard(e) {
      e.preventDefault();
      const new_x = e.clientX;
      const new_y = e.clientY;
      this.change_x = this.start_x - new_x;
      this.change_y = this.start_y - new_y;

      this.start_x = e.clientX;
      this.start_y = e.clientY;

      // We constantly increment or decrement offset values by 1
      this.draggable.style.left = (this.draggable.offsetLeft - this.change_x) + "px";
      this.draggable.style.top = (this.draggable.offsetTop - this.change_y) + "px";
    },
    stopDrag(e) {
      e.preventDefault();
      document.onmousemove = null;
    }
  }
}
</script>

<style>
  body {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    background: lightgoldenrodyellow;
  }

  .draggables-container {

  }

  .card {
    position: absolute;
    cursor: pointer;
    display: inline-block;
    padding: 20px;
    background: lightskyblue;
  }
</style>
