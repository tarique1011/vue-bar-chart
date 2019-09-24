<template>
  <div id="app">
    <div
      class="bar-chart-container"
      :style="{width: getContainerWidth(), height: getContainerHeight()}"
    >
      <div class="left-container">
        <span class="xlabel">{{ xlabel }}</span>
      </div>
      <div class="right-container">
        <div class="bars-container">
          <ul class="bar-list">
            <Bar
              v-for="(option,index) of options"
              :key="index"
              :width="getWidth()"
              :height="getHeight(option.value)"
              :title="option.title"
              :value="option.value"
              :color="option.color"
            />
          </ul>
        </div>
        <span class="ylabel">{{ ylabel }}</span>
      </div>
    </div>
  </div>
</template>

<script>
import Vue from "vue";
import Component from "vue-class-component";
import Bar from "./Bar.vue";

@Component({
  components: {
    Bar
  },
  props: {
    xlabel: {
      type: String,
      default: "xlabel"
    },
    ylabel: {
      type: String,
      default: "ylabel"
    },
    height: {
      type: Number,
      default: 400
    },
    width: {
      type: Number,
      default: 400
    },
    options: {
      type: Array,
      required: true
    }
  }
})
class BarChart extends Vue {
  created() {
    let maxBarHeight = this.getMaxValue();
    this.heightFactor = this.getHeightFactor(maxBarHeight);
  }

  getMaxValue() {
    let maxValue = Math.max.apply(
      Math,
      this.options.map(function(option) {
        return option.value;
      })
    );
    return maxValue;
  }

  getHeightFactor(maxHeight) {
    let factor = (0.85 * this.height) / maxHeight;
    return factor;
  }

  getHeight(value) {
    return this.heightFactor * value;
  }

  getWidth() {
    let bars = this.options.length;

    let barWidth = (1 / bars) * 0.85 * this.width;
    barWidth = barWidth - 0.01 * 0.85 * this.width;

    return barWidth;
  }

  getContainerWidth() {
    return this.width + "px";
  }

  getContainerHeight() {
    return this.height + "px";
  }
}

export default BarChart;
</script>
