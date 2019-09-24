<template>
  <div class="bar" @mouseover="displayValue()" @mouseleave="hideValue()">
    <canvas ref="myCanvas" :height="height" :width="width" />
    <div
      class="value"
      :style="{backgroundColor: valueBackgroundColor, color: valueTextColor }"
      v-if="showValue"
    >{{ title}}({{ value }})</div>
  </div>
</template>

<script>
import Vue from "vue";
import Component from "vue-class-component";

@Component({
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
    },
    valueBackgroundColor: {
      type: String,
      required: false,
      default: "#4287f5"
    },
    valueTextColor: {
      type: String,
      required: false,
      default: "#ffffff"
    }
  }
})
class Bar extends Vue {
  canvas = null;

  showValue = false;

  displayValue() {
    this.showValue = true;
  }

  hideValue() {
    this.showValue = false;
  }

  mounted() {
    this.canvas = this.$refs.myCanvas;

    const ctx = this.canvas.getContext("2d");
    ctx.beginPath();
    ctx.rect(0, 0, this.width, this.height);
    ctx.fillStyle = this.color;

    ctx.fill();
  }
}

export default Bar;
</script>

<style scoped>
.bar {
  margin-right: 2%;
}

.bar:hover {
  cursor: pointer;
}

.value {
  position: absolute;
  bottom: 10;
  padding: 5px;
  border-radius: 5px;
}
</style>
