<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-title>💰 Currency converter</ion-title>
      </ion-toolbar>
    </ion-header>
    
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">IoniK Fixer</ion-title>
        </ion-toolbar>
      </ion-header>
    
      <div id="container">
        <Search
          :devices="devices"
          @convert="sendData"
        ></Search>
        <Results
          v-if="convert.symbol"
          :convert="convert"
        ></Results>
        
      </div>
    </ion-content>
  </ion-page>
</template>

<script>
import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar } from '@ionic/vue';
import { defineComponent } from 'vue';
import Search from "../../src/Components/Search";
import Results from "../../src/Components/Results";

export default defineComponent({
  name: 'Home',
  components: {
    IonContent,
    IonHeader,
    IonPage,
    IonTitle,
    IonToolbar,
    Search,
    Results
  },
  data(){
    return {
      convert: {
        symbol: "",
        montant: ""
      },
      devices: [],
    }
  },
  mounted(){
    this.fetchDevice()
  },
  methods: {
    fetchDevice(){
      fetch(`http://data.fixer.io/api/symbols?access_key=${process.env.VUE_APP_API_KEY}`)
      .then(res => res.json())
      .then(symbols => {
          this.devices = symbols.symbols
          this.error = ""
      })
    },
    sendData(convert){
      this.convert = convert
    }
  },
});
</script>

<style scoped>

</style>