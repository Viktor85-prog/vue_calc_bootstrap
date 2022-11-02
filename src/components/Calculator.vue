<template>
  <div class="p-3 calc">
	<div class="w-full rounded m-1 p-3 text-right lead font-weight-bold text-white bg-vue-dark">
		{{calcValue || 0}}
	</div>
  
	<div class="row no-gutters">
		<div class="col-3" v-for="el in calcElements" :key=el>
			<div class="lead text-white text-center m-1 py-3 bg-vue-dark rounded hover-class"
			:class="{'bg-vue-green':['C','*','/','-','+','%','='].includes(el)}"
			@click="action(el)"
			>
				{{el}}
			</div>
		</div>
	</div>
  </div>
</template>

<script>
export default {
  name: 'Calculator-component',
  props: {
    msg: String
  },

  data() {
	return {
		calcValue:'',
		calcElements: ['C','*','/','-',7,8,9,'+',4,5,6,'%',1,2,3,'=',0,'.'],
		operator: null,
		prevCalcValue:''
		}
  },

  methods: {
	action(el) {
		if(!isNaN(el) || el === '.') {
			this.calcValue += el +''
		}

		if(el === 'C') {
			this.calcValue = ''
		}

		if(el === '%') {
			this.calcValue = this.calcValue / 100 + ''
		}

		if(['*','/','-','+'].includes(el)) {
			this.operator = el
			this.prevCalcValue = this.calcValue
			this.calcValue =''
		}

		if(el === '=') {
			this.calcValue = eval(
				this.prevCalcValue + this.operator + this.calcValue
			)

			this.prevCalcValue = ''
			this.operator = null
		}
	}
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calc {
	max-width: 400px;
	margin: 50px auto;
	background: #234;
}

.bg-vue-dark {
	background: #31475e;
}

.hover-class:hover{
	cursor: pointer;
	background: #3D5875;
}

.bg-vue-green {
	background: #3fb984;
}
</style>
