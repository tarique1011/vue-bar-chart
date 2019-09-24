<template>
  <div id="app">
    <BarChart
      :options="this.options"
      xlabel="Marks"
      ylabel="Subjects"    
    />
  </div>
</template>

<script>
import Vue from "vue";
import Component from "vue-class-component";
import BarChart from "./components/BarChart.vue";

@Component({
  components: {
    BarChart
  }
})
class App extends Vue {
  width = 600;
  height = 800;

  options = [
    {
      title: "Maths",
      value: 500,
      color: "#545D79"
    },
    {
      title: "Chemistry",
      value: 55,
      color: "#8AB721"
    },
    {
      title: "Physics",
      value: 460,
      color: "#C77D99"
    },
    {
      title: "Ecomonics",
      value: 100,
      color: "#78CAE3"
    },
    {
      title: "English",
      value: 370,
      color: "#E64A33"
    },
    {
      title: "Maths",
      value: 500,
      color: "#545D79"
    },
    {
      title: "Chemistry",
      value: 55,
      color: "#8AB721"
    },
    {
      title: "Physics",
      value: 460,
      color: "#C77D99"
    },
    {
      title: "Ecomonics",
      value: 100,
      color: "#78CAE3"
    },
    {
      title: "English",
      value: 370,
      color: "#E64A33"
    },
  ];
}

export default App;
</script>
