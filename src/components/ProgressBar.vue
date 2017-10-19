<template>
<div class="progress-container">
  <div :class="className" @click="changeValue()"></div>
</div>
</template>

<script>
import Progress from 'progressbar.js';

export default {
  props: ["id", 'progress'],

  data() {
    return {
      progressBar: null,
      options: {
        color: 'red',
        strokeWidth: 15,
        trailWidth: 15,
        trailColor: '#ddd',
        duration: 1400,
        easing: "easeOut",
        text: {
          value: '0',
          alignToBottom: false
        }
      },
			value: this.progressProp
    }
  },

  methods: {

		/**
		* Main function to change the value of the progress bar. May want to consider a better constructor based method for this.
		*/
    setProgress(val) {
      this.progressBar.setText((val * 100).toFixed(0));
      this.options.duration = 1400;
      this.progressBar.text.style.color = this.getColor(val);
      this.progressBar.animate(val, this.options);
      this.progressBar.path.setAttribute('stroke', this.getColor(val));

    },

		/**
		*  Temp function. Don't really need this.
		*/
    changeValue() {
      let value = this.progressBar.value();
      if (value > 0) {
        value -= .1
        this.setProgress(value);
      }
    },

		/**
		* Returns a HSL value on linear scale from 2 hex codes to avoid muddy colors
		*/
    getColor(value, from = 120, to = 0) {
      let range = to - from;
      let result = (range * (1 + value)) + range;
      let color = "hsl(" + result + ", 100%, 40%)";
      return color;
    }

  },

  computed: {
    /**
     * Give the components unique ID as a prop and a class for general styling
     */
    className() {
      return "progress progress-" + this.id;
    },

		progressProp(){
			return this.progress;
		}
  },

	watch:{
		progressProp(newVal){
			this.value = newVal;
			this.setProgress(newVal);
		}

	},

  mounted() {
    // Create the Progress bar
		this.value = this.progressProp;
    this.progressBar = new Progress.SemiCircle('.progress-' + this.id, this.options);
    this.setProgress(this.value);
  },

}
</script>

<style>
	.progress {
	  box-sizing: border-box;
	  /*width: 33%;*/
	  margin: 20px auto;
	}

	.progressbar-text {
	  font-size: 2.5em;
	  position: static !important;
	  margin-top: -1em !important;
	  transform: none !important;
	  text-align: center;
	}
</style>
