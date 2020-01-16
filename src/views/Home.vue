<template>
  <div>
    <ion-header>
      <ion-toolbar>
        <ion-title>ZaggaDat</ion-title>
      </ion-toolbar>
    </ion-header>
    <div class="ion-padding">
      <zipsearch v-on:get-zip="getZipInfo"/>
    </div> 
    
  </div>
</template>

<script>
// @ is an alias to /src
//import HelloWorld from '@/components/HelloWorld.vue'
import zipsearch from "@/components/zipsearch.vue"

export default {
  name: 'home',
  components: {
    zipsearch
  },
  methods:{
     showAlert() {
      return this.$ionic.alertController
        .create({
          header: "Error",
          message: "Please enter valid Us Zipcode",
          buttons: ["OK"]
        })
        .then(a => a.present());
    },
   async getZipInfo(zip){
      const res = await fetch(`https://api.zippopotam.us/us/${zip}`)
      if(res.status == 404){
        this.showAlert();
      }
      else{
        this.info=await res.json()
        console.log(this.info)
      }
    },
    data() {
      return {
        info:null
      }
    },
  }
}
</script>
