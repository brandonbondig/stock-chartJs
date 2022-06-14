
<template>
    <div>
        
    </div>
</template>
<script>
import axios from 'axios'

export default {
    name: 'getIndicator',
    props: ['stock','indicator'.toLocaleLowerCase(), 'period', 'priceAction'],
    data() {
        return {
            loaded:false
        }
    },
    async mounted() {

        this.loaded = false;

        //Stock Change
        const data = await axios.get(
            `https://financialmodelingprep.com/api/v3/technical_indicator/daily/${this.stock}?period=${this.period}&type=${this.indicator}&apikey=35e33a36772591c05fee85991577dbe0`
        );
        console.log(data.data);
        this.loaded = true;

    },
}
</script>

<style>
</style>