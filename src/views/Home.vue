<template>
  <div>
    <ion-header>
      <ion-toolbar>
        <ion-title>ZaggaDat</ion-title>
      </ion-toolbar>
    </ion-header>
    <div class="ion-padding">
      <zipsearch v-on:get-zip="getZipInfo" />
      <display v-bind:info="info" />
      <ion-button color="light" expand="block" v-if="info" @click="clear">
        Clear
      </ion-button>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
//import HelloWorld from '@/components/HelloWorld.vue'
import zipsearch from "@/components/zipsearch.vue";
import display from "@/components/display.vue";

export default {
  name: "home",
  components: {
    zipsearch,
    display
  },
  data() {
    return {
      info: null
    };
  },
  methods: {
    showAlert() {
      return this.$ionic.alertController
        .create({
          header: "Error",
          message: "Please enter valid Us Zipcode",
          buttons: ["OK"]
        })
        .then(a => a.present());
    },
    async getZipInfo(zip) {
      const res = await fetch(`https://api.zippopotam.us/us/${zip}`);
      if (res.status == 404) {
        this.showAlert();
      } else {
        this.info = await res.json();
        //console.log(this.info)
      }
    },
    clear() {
      this.info = null;
    }
  }
};
</script>
