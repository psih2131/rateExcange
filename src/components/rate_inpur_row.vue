<template>
	<div class="exchange-counter__money-row" >
		<input type="text"  placeholder="0"  v-model="currentValueExchan" onkeyup="this.value = this.value.replace(/[^\d]/g,'');">
		<div class="exchange-counret__value">{{roundedNumber()}}</div>
		<p class="exchange-counter__name">{{rateProps.ccy}} / {{rateProps.base_ccy}}</p>
	</div>
</template>

<script>
	export default{
		props: {
			rateProps:{
				type: Object,
				reqired: true
			}
		},
		data(){
			return{
				currentValueExchan: 1,
			}
		},
		methods:{
			roundedNumber() {
				let x = this.currentValueExchan*this.rateProps.buy
				return x.toFixed(2)
			}
		}
	}
</script>
