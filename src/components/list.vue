<template>
	<div class="row-rate" >
     	<div class="row-rate__box">{{listprops.currency}}</div>
     	<div class="row-rate__box">{{listprops.purchaseRateNB}}</div>
     	<div class="row-rate__box">{{listprops.saleRateNB}}</div>
   </div>
</template>

<script>
	export default{
		props: {
			listprops:{
				type: Object,
				reqired: true
			}
		}
	}
</script>