<template>
<div id="app">
    <city-picker @closeModal='closeModal' @setRootCodes='setRootCodes'></city-picker>
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
        closeModal();
      },
      setRootCodes(codes){
        this.codes = codes;
        getCodes(codes);
      }
    }
}
</script>
