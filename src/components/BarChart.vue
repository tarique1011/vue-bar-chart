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
              :width="getBarWidth()"
              :height="getBarHeight(option.value)"
              :title="option.title"
              :value="option.value"
              :color="option.color"
              :valueBackgroundColor="valueBackgroundColor"
              :valueTextColor="valueTextColor"
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
    },
    valueBackgroundColor: {
      type: String,
      required: false
    },
    valueTextColor: {
      type: String,
      required: false
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

  getBarHeight(value) {
    return this.heightFactor * value;
  }

  getBarWidth() {
    let bars = this.options.length;

    let barWidth = (1 / bars) * 0.85 * this.width;
    barWidth = barWidth - 0.02 * 0.85 * this.width;

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

<style>
ul {
  padding: 0px;
  margin: 0px;
}

.bar-chart-container {
  display: flex;
  flex-direction: row;
  align-items: center;
}

.left-container {
  width: 10%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.xlabel {
  text-align: center;
  writing-mode: vertical-rl;
  transform: rotate(180deg);
  font-weight: 700;
}

.right-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  width: 90%;
  height: 100%;
}

.bars-container {
  padding: 10px 0px 0px 10px;
  height: 85%;
  width: 95%;
  border-left: #000 solid 1px;
  border-bottom: #000 solid 1px;
}

.bar-list {
  display: flex;
  flex-direction: row;
  align-items: flex-end;
  justify-content: flex-start;
  width: 100%;
  height: 100%;
}

.ylabel {
  height: 10%;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  font-weight: 700;
}
</style>