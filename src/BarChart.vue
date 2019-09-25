<template>
  <div
    class="bar-chart-container"
    :style="{width: getContainerWidth(), height: getContainerHeight()}"
  >
    <div class="left-container">
      <span class="ylabel">{{ ylabel }}</span>
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
          />
        </ul>
      </div>
      <span class="xlabel">{{ xlabel }}</span>
    </div>
  </div>
</template>

<script>
import Bar from "./Bar.vue";

export default {
  name: "BarChart",
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
  },
  components: {
    Bar
  },
  methods: {
    //get the maximum value among the options for scaling
    getMaxValue() {
      let maxValue = Math.max.apply(
        Math,
        this.options.map(function(option) {
          return option.value;
        })
      );
      return maxValue;
    },

    //get the scale factor for the height of each bar
    getHeightFactor(maxHeight) {
      let factor = (0.85 * this.height - 10) / maxHeight;
      return factor;
    },

    getBarHeight(value) {
      let maxValue = this.getMaxValue();
      let heightFactor = this.getHeightFactor(maxValue);
      return heightFactor * value;
    },

    getBarWidth() {
      let bars = this.options.length;

      let barWidth = (1 / bars) * 0.85 * this.width;
      barWidth = barWidth - 0.02 * 0.85 * this.width;

      return barWidth;
    },

    getContainerWidth() {
      return this.width + "px";
    },

    getContainerHeight() {
      return this.height + "px";
    }
  }
};
</script>

<style lang="css" scoped>
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

.ylabel {
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

.xlabel {
  height: 10%;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  font-weight: 700;
}
</style>