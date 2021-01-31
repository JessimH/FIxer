<template>
    <ion-card>
        <ion-card-header>
            <ion-card-subtitle>{{convert.montant}}€ to {{convert.symbol}}</ion-card-subtitle>
            <ion-card-title>{{result}} {{convert.symbol}}</ion-card-title>
        </ion-card-header>
  </ion-card>
</template>

<script>
import { IonCard, IonCardTitle, IonCardSubtitle } from '@ionic/vue';

export default({
    name: "Results",
    components: { 
        IonCard, 
        IonCardTitle, 
        IonCardSubtitle
        },        
    data(){
        return{
            result: ""
        }
    },
    mounted(){
        this.Convert()
    },
    props: ['convert'],
    methods: {
        Convert(){
            fetch(`http://data.fixer.io/api/latest?access_key=${process.env.VUE_APP_API_KEY}&symbols=${this.convert.symbol}`)
            .then(res => res.json())
            .then(result => {
                let rates = Object.values(result.rates)
                this.result = Math.round((this.convert.montant * rates[0]) *100) / 100
                console.log(rates)
                console.log(this.result)
            })
        }
    },
    watch: {
        convert: {
            deep: true,
            handler(){
                this.Convert();
            }
        }
    },
});
</script>

<style scoped>

</style>