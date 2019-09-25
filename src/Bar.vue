<template>
  <div class="bar" @mouseover="displayValue()" @mouseleave="hideValue()">
    <canvas ref="myCanvas" :height="height" :width="width" />
    <div class="value" v-if="showValue">{{ title}}({{ value }})</div>
  </div>
</template>

<script>
export default {
  name: "Bar",
  props: {
    title: {
      type: String,
      required: true
    },
    value: {
      type: Number,
      required: true
    },
    color: {
      type: String,
      required: true,
      default: "#787878"
    },
    height: {
      type: Number,
      required: true
    },
    width: {
      type: Number,
      required: true
    }
  },
  data() {
    return {
      canvas: null,
      showValue: null
    };
  },
  mounted() {
    this.drawCanvas();
  },
  updated() {
    this.drawCanvas();
  },
  methods: {

    drawCanvas() {
      this.canvas = this.$refs.myCanvas;
      const ctx = this.canvas.getContext("2d");
      ctx.beginPath();
      ctx.rect(0, 0, this.width, this.height);
      ctx.fillStyle = this.color;
      ctx.fill();
    },

    //show value of bar on mouse hover
    displayValue() {
      this.showValue = true;
    },

    //hide value of bar when mouse leaves
    hideValue() {
      this.showValue = false;
    }
  }
};
</script>

<style lang="css" scoped>
.bar {
  margin-right: 2%;
}

.bar:hover {
  cursor: pointer;
}

.value {
  position: absolute;
  bottom: 10;
  background-color: #000000;
  color: #ffffff;
  padding: 5px;
  border-radius: 5px;
}
</style>
