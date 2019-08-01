<template>
  <div class="ion-page">
    <ion-header>
      <ion-toolbar>
        <ion-title>Zip Info</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content class="ion-padding">
      <ZipSearch @get-zip="getZipInfo"/>
    </ion-content>
  </div>
</template>

<script>
import ZipSearch from '../components/ZipSearch'
export default {
  name: "home",
  components:{
    ZipSearch
  },
  methods: {
    async getZipInfo(zip){
      const res = await fetch(`https://api.zippopotam.us/us/${zip}`);

      if(res.status === 404){
        this.showAlert();
      }
      const info = await res.json();

      console.log(info)

    },
    showAlert(){
            return this.$ionic.alertController
            .create({
                header: "Not Valid",
                message: "Please enter a valid zipcode",
                buttons: ["OK"]
            })
            .then(a => a.present());
        }
  },
};
</script>
