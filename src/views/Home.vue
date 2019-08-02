<template>
  <div class="ion-page">
    <ion-header>
      <ion-toolbar>
        <ion-title>Zip Info</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content class="ion-padding">
      <ZipSearch @get-zip="getZipInfo"/>
      <ZipInfo :info="info"/>
      <ClearInfo :info="info" v-on:clear-info="clearInfo"/>
    </ion-content>
  </div>
</template>

<script>
import ZipSearch from '../components/ZipSearch'
// import axios from 'axios'
import ZipInfo from '../components/ZipInfo'
import ClearInfo from '../components/ClearInfo'

export default {
  name: "home",
  data(){
    return{
      info: null
    }
  },
  components:{
    ZipSearch,
    ZipInfo,
    ClearInfo,
  },
  methods: {
    async getZipInfo(zip){
      const res = await fetch(`https://api.zippopotam.us/us/${zip}`);

      if(res.status === 404){
        this.showAlert();
      }
      this.info = await res.json();
      // console.log(this.info)
    },
    showAlert(){
        return this.$ionic.alertController
        .create({
            header: "Not Valid",
            message: "Please enter a valid zipcode",
            buttons: ["OK"]
        })
        .then(a => a.present());
    },
    clearInfo(){
      this.info = null
    }
  },
};
</script>
