<template>
	<div class="exchange-counter__money-row" >
		<input type="text"  placeholder="0"  v-model="currentValueExchan" onkeyup="this.value = this.value.replace(/[^\d]/g,'');">
		<div class="exchange-counret__value">{{currentValueExchan*rateProps.buy}}</div>
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
				currentValuePrice: 1,
			}
		},
		methods:{
		}
	}
</script>
