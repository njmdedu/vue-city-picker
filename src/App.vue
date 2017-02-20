<template>
<div id="app">
    <city-picker @closeModal='closeModal' @setRootCodes='setRootCodes' v-bind:data-codes="codes"></city-picker>
</div>
</template>

<script>
import Citypicker from './assets/components/city-picker.vue';
export default {
    name: 'app',
    data(){
      return {
        codes:''
      }
    },
    components: {
        'city-picker': Citypicker
    },
    methods:{
      closeModal(){
        $.closePopup();
      },
      setRootCodes(codes){
        this.codes = codes;
        test();
      }
    }
}
</script>
