<template>
  <div id="app">
    <div>
      <p>
        Your place here
        <input type="number" min="1" max="10" step="1" v-model.number="num">
      </p>
      <h2>Congratulations!</h2>
      <p v-color="'red'">You won <span>{{ num | award }} place!</span></p>
    </div>
  </div>
</template>

<script>
import Vue from 'vue'

Vue.directive('color', {
	bind(el, binding){
		el.style.color = binding.value
	}
})

export default {
  name: 'App',
  data(){
    return {
      num: 2,
    }
  },
  filters: {
    award(value){
      let returnValue = '';
      switch (value){
        case 1:
          returnValue = `${value}st`
          break;
        case 2:
          returnValue = `${value}nd`
          break;
        case 3:
          returnValue = `${value}rd`
          break;
        default:
          return `${value}th`
      }
      return returnValue;
    }
  },
}
</script>
