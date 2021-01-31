<template>
    <div id="container">
        <ion-item>
          <ion-label position="stacked">Montant</ion-label>
          <ion-input type="number" v-model="convert.montant" placeholder="EUR"></ion-input>
        </ion-item>

        <ion-item>
          <ion-label>En </ion-label>
          <ion-select v-model="selectedDevice" ok-text="Okay" cancel-text="Dismiss">
            <ion-select-option v-for="device in devices" :key="device" :value="device" >
                {{device}}
            </ion-select-option>
          </ion-select>
        </ion-item>

        <ion-button :disabled="!convert.montant || !selectedDevice" @click="SendData" expand="block" class="md button button-block button-solid ion-activatable ion-focusable hydrated">Convertir</ion-button>

    </div>
</template>

<script>
import { IonInput, IonSelect, IonSelectOption, IonItem, IonLabel } from '@ionic/vue';

export default ({
  components: { 
      IonInput, 
      IonItem,
      IonSelectOption,
      IonSelect,
      IonLabel
    },
    name: "Search",
    mounted(){
    },
    props: ['devices'],
    data(){
        return {
            selectedDevice: "",
            convert: {
                symbol: "",
                montant: ""
            },
        }
    },
    methods: {
        SendData(){
            this.convert.symbol = Object.keys(this.devices).find(key => this.devices[key] === this.selectedDevice)
            this.$emit('convert', this.convert)
        }
    }
})
</script>

<style scoped>
.form{
    display:flex;
    flex-direction: column;
}
</style>