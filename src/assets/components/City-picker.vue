<template lang="html">
  <div class="root">
    <div class="col province">
      <ul>
        <li v-for="province in getProvinces()">
          <span class="txt">{{province.name}}</span>
        </li>
      </ul>
    </div>
    <div class="col city">

    </div>
    <div class="col district">

    </div>
  </div>
</template>

<script>
import citydata from './../city-datas'
export default {
    data() {
        return {
            citydata: citydata.citydata
        }
    },
    methods: {
        getProvinces() {
            var procinces = [];
            console.log(citydata)
            $.each(this.citydata, function(index, obj) {
                procinces.push({
                    name: obj.name,
                    code: obj.code,
                    sub: obj.sub
                });
            });
            return procinces;
        }
    }
}
</script>

<style lang="css">
  .root{
    width: 100%;
    display: flex;
    align-items: center;
  }
  .col{
    width:33.3333%;
  }
  .province {

  }

  .province ul{

  }

  .province ul li{
    float: none;
  }

  .province ul li .txt{
    font-size: 1rem;
  }
</style>
