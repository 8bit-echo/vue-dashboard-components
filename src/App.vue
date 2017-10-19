<template>
<div id="app">

  <draggable :list="panes" class="row center component">
    <dash-pane v-for="pane, i in panes" :key="pane.id" :color="pane.id">{{ pane.id + 1 }}</dash-pane>
  </draggable>

  <div class="row">
    <div class="col component" id="progressBar">
      <progress-bar :id="1" :progress="progress"></progress-bar>
      <div class="control row between">
        <button @click="progress -= .1"><b> - 10% </b></button>
        <button @click="progress += .1"><b> + 10% </b></button>
      </div>
    </div>

    <div class="row component" style="width:50%">
      <pie-chart :data="pieChartData" :config="pieChartConfig"></pie-chart>
    </div>

  </div>

</div>
</template>

<script>
import Pane from './components/Pane';
import vuex from 'vuex';
import draggable from 'vuedraggable';
import progress from './components/ProgressBar';
const d3 = require('d3');
import {  vueChartPie } from 'd2b';

export default {
  name: 'app',

  data() {
    return {
      // Draggable component
      panes: [{
          name: 'one',
          id: 0
        },
        {
          name: 'two',
          id: 1
        },
        {
          name: 'three',
          id: 2
        }
      ],
      // Progress bar
      progress: .5,
      // Pie Chart
      pieChartData: [{
          label: 'arc 1',
          value: 23
        },
        {
          label: 'arc 2',
          value: 31
        },
        {
          label: 'arc 3',
          value: 80
        },
        {
          label: 'arc 4',
          value: 8
        }
      ],
      pieChartConfig: (chart) => {
	      chart.donutRatio(.5);
	      chart.color = "ff000000ff000000ff";
	    }
    }
  },

  computed: {

  },

  components: {
    dashPane: Pane,
    draggable,
    progressBar: progress,
    pieChart: vueChartPie
  }
}
</script>

<style>
body {
  font-family: sans-serif;
}
</style>
