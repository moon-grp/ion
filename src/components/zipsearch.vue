<template>
  <ion-grid>
    <form @submit="onSubmit">
      <ion-col>
        <ion-item>
          <ion-input
            placeholder="Enter U.S Based ZipCode"
            name="zip"
            :value="zip"
            @input="zip = $event.target.value"
          >
          </ion-input>
        </ion-item>
      </ion-col>
      <ion-col>
        <ion-button type="submit" color="primary" expand="block"
          >Find</ion-button
        >
      </ion-col>
    </form>
  </ion-grid>
</template>

<script>
export default {
  name: "zipsearch",
  data() {
    return {
      zip: ""
    };
  },
  methods: {
    onSubmit(e) {
      e.preventDefault();
      const isVaildZip = /(^\d{5}$)|(^\d{5}-\d{4}$)/.test(this.zip);
      if (!isVaildZip) {
        this.showAlert();
        this.zip=""
      } else {
        this.$emit("get-zip", this.zip)
        this.zip=""
      }
    },
    showAlert() {
      return this.$ionic.alertController
        .create({
          header: "Error",
          message: "Please enter valid Zipcode",
          buttons: ["OK"]
        })
        .then(a => a.present());
    }
  }
};
</script>
