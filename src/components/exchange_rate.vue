<template>
 <div class="rate-component">
  <div class="rate-component__btn-row">
    <button class="btn-rate pb">Курс НБ</button>
    <div class="date-value-row">
      <p>Дата курса: {{currentDate}}</p>
      <input type="date" v-model="selectDate" @change="changeDateF()">
    </div>
  </div>

   <div class="rate-component__header-row row-rate">
     <div class="row-rate__box">Валюта</div>
     <div class="row-rate__box">Покупка</div>
     <div class="row-rate__box">Продажа</div>
   </div>
   <div class="errorLoad" :class="{errorLoadActive: activError}">{{errorLoad}}</div>

   <list v-for="list in listRate" :key="list.id" :listprops="list" />
   
 </div>
</template>

<script>
	import listRates from '@/components/list.vue'
	export default{
		components: {
		   list: listRates
		},
		data(){
			return{
				currentDate: '',
				selectDate: '',
				listRate: [],
				errorLoad: '',
				activError: false,
			}
		},
		methods: {
			currentDateF(){
				let dateObj = new Date();
				let month = dateObj.getUTCMonth() + 1; //months from 1-12
				let day = dateObj.getUTCDate();
				let year = dateObj.getUTCFullYear();
				this.currentDate = `${day}.${month}.${year}`
			},

			changeDateF(){
				this.$emit('preloaderStarus', false)
				let selectDateInput = this.selectDate
				let year = selectDateInput.substr(0,4);
				let mounts = selectDateInput.substr(5,2);
				let day = selectDateInput.substr(8,2);
				let newDate = `${day}.${mounts}.${year}`

				this.currentDate = newDate
				this.apiFunction(newDate);
			},

			apiFunction(datemain){
				fetch(`https://cors-anywhere.herokuapp.com/https://api.privatbank.ua/p24api/exchange_rates?json&date=${datemain}`)
			    .then(response => {
				    if (response.status !== 200) {
				      this.errorLoad = 'Ошибка загрузки данных, по текущей дате не найдено записей в архиве, выберите другую дату или дождитесь когда архив обновит данные'
							this.listRate = []
							this.activError = true;
							this.$emit('preloaderStarus', true)
				    }
				    else{
				    	return response.json()
				      .then(data =>{
				    	this.dataFetchRender(data)
				    	this.activError = false;
				    	this.$emit('preloaderStarus', true)
				    })
				    }
			    })
			    .catch(error => {
		        console.log(error);
		      });
			},

			dataFetchRender(alldata){
				let arrayRate = alldata.exchangeRate;
				this.errorLoad = ''
				this.listRate = arrayRate
			}
		},

		created(){
			this.currentDateF();
		},

		mounted() {
			this.$nextTick(function () {
				this.apiFunction(this.currentDate)
			})
		}

	}
</script>

<style></style>
