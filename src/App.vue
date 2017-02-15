<template>
<div id="app">
    <city-picker></city-picker>
</div>
</template>

<script>
import Citypicker from './assets/components/City-picker.vue';
export default {
    name: 'app',
    components: {
        'city-picker': Citypicker
    },
    data() {
        return {
            msg: 'Vue-CityPicker'
        }
    }
}
</script>

<style>
@media only screen and (min-width: 320px) {
    html {
        font-size: 12px !important;
        /*10 ÷ 16 × 100% = 62.5%*/
    }
}

@media only screen and (min-width: 370px) {
    html {
        font-size: 13px !important;
    }
}

@media only screen and (min-width: 410px) {
    html {
        font-size: 15px !important;
    }
}

@media only screen and (min-width: 481px) {
    html {
        font-size: 23px !important;
    }
}

body {
    font-family: '黑体';
}

* {
    margin: 0;
    padding: 0;
}

h1,
h2 {
    font-weight: normal;
}

ul {
    list-style-type: none;
    padding: 0;
}

li {
    display: inline-block;
    padding: 0 10px;
}

a {
    color: #42b983;
}
#app{
  background: #fff;
}
</style>
