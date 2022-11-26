<template>
  <section class="exchange-rate">
   <div class="main-wrapper">
     <div class="app-title">
       <div class="app-title__image">
         <img src="https://cdn.privat24.ua/icons/file/ServiceCurrency.svg" alt="">
       </div>
       <h1 class="app-title__text">Курс валют</h1>
     </div>

     <rate @preloaderStarus="preloaderSwitch" />
     
     <counter @preloaderStarus="preloaderSwitch" />

   </div>
  </section>

  <div class="preloader-conteiner" :style="styleObject">
    <div class="preloader">
      <div class="sk-chase">
        <div class="sk-chase-dot"></div>
        <div class="sk-chase-dot"></div>
        <div class="sk-chase-dot"></div>
        <div class="sk-chase-dot"></div>
        <div class="sk-chase-dot"></div>
        <div class="sk-chase-dot"></div>
      </div>
    </div>  
  </div>
  
</template>

<script>
import exchangeRate from '@/components/exchange_rate.vue'
import counterComponent from '@/components/counter.vue'

export default {
  name: 'App',
  components: {
   rate: exchangeRate,
   counter: counterComponent
  },
  data(){
    return{
      styleObject: {
          display: 'flex',
        },
    }
  },
  methods: {
    preloaderSwitch(status){
      if(status == true){
        this.styleObject = {
          display: 'none'
        }
      }
      else{
        this.styleObject = {
          display: 'flex'
        }
      }
    }
  }
}
</script>

<style lang="scss">

</style>
