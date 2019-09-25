# vue-bar-chart

vue-bar-chart is a customized bar chart component to showcase statistical data in a clean way.

### Install

```
cd vueproject
npm install --save vue-bar-chart
```

### Usage 

```javascript
<template>
  <div id="app">
    <BarChart 
      :options="options" 
      :width="width"  //default is 400px
      :height="height" //default is 400px
      xlabel="Stock Prices($)" 
      ylabel="Year" />
  </div>
</template>

<script>
import BarChart from "vue-bar-chart";

export default {
  name: "app",
  components: {
    BarChart
  },
  data() {
    return {
      width: 600,
      height: 600,
      options: [
        {
          title: "2015",
          value: 90,
          color: "#a86f32"
        },
        {
          title: "2016",
          value: 70,
          color: "#545D79"
        },
        {
          title: "2017",
          value: 95,
          color: "#8AB721"
        },
        {
          title: "2018",
          value: 40,
          color: "#32a852"
        },
        {
          title: "2019",
          value: 60,
          color: "#4832a8"
        }
      ]
    };
  }
};
</script>
```

For visual representation please visit https://modest-poincare-6995f6.netlify.com
