<template>
	 <div class="exchange-counter" >
	 	<h2 class="exchange-counter__title">Калькулятор расчета на сегодня</h2>
	 	<div class="exchange-counter__type-row">
	 		<button class="btn-rate" :class="{ 'btn-rate_active': isActiveBtNzNal }" @click="typeChangeBezNal()">Безналичный обмен</button>
	 		<button class="btn-rate" :class="{ 'btn-rate_active': isActiveBtNal }" @click="typeChangeNal()">Наличный обмен</button>
	 	</div>

	 	<p class="status-change-nam">На сегодня в банке для обмена доступно <span>{{arrayRateCouner.length}}</span> валюты</p>

	 	<inputrow  v-for="item in arrayRateCouner" :key="item.id" :rateProps="item" />

	 </div>
</template>

<script>
	import inputExchangerRow from '@/components/rate_inpur_row.vue'
	export default{
		components: {
		   inputrow: inputExchangerRow
		},
		data(){
			return{
				apiKeyNal: 'https://cors-anywhere.herokuapp.com/https://api.privatbank.ua/p24api/pubinfo?json&exchange&coursid=5',
				apiKeyBeznal: 'https://cors-anywhere.herokuapp.com/https://api.privatbank.ua/p24api/pubinfo?exchange&json&coursid=11',
				arrayPrise1: [],
				arrayRateCouner: [],
				isActiveBtNzNal: true,
				isActiveBtNal: false,
				statusPreloader: false,
			}
		},
		methods:{
			apiFunctionCounner(apiKey , preloaderValue){
				fetch(apiKey)
			    .then(response => {
			    	return response.json();
			    })
			    .then(data =>{
			    	this.dataCounterRender(data)
			    	if(preloaderValue == true){
			    		this.$emit('preloaderStarus', true)
			    		this.statusPreloader = false
			    	}
			    	
			    });

			},

			dataCounterRender(serveData){
				this.arrayRateCouner = []
				for(let i = 0; i < serveData.length; i++){
					this.arrayRateCouner.push(serveData[i])
					console.log(serveData[i])
				}
			},

			typeChangeNal(){
				this.statusPreloader = true;
				let preloaderValue = this.statusPreloader;
				this.$emit('preloaderStarus', false)
				this.apiFunctionCounner(this.apiKeyNal, preloaderValue);
				this.isActiveBtNal = true;
				this.isActiveBtNzNal = false;
				
			},
			typeChangeBezNal(){
				this.statusPreloader = true;
				let preloaderValue = this.statusPreloader;
				this.$emit('preloaderStarus', false)
				this.apiFunctionCounner(this.apiKeyBeznal, preloaderValue);
				this.isActiveBtNal = false;
				this.isActiveBtNzNal = true;
			},

		},
		mounted(){
			this.$nextTick(function () {
				this.apiFunctionCounner(this.apiKeyBeznal, this.statusPreloader);
			})
		}
	}
</script>

<style>
	
</style>