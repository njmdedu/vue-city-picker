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
      <ul>
        <li v-for="province in getProvinces()">
          <span class="txt">{{province.name}}</span>
        </li>
      </ul>
    </div>
    <div class="col district">
      <ul>
        <li v-for="province in getProvinces()">
          <span class="txt">{{province.name}}</span>
        </li>
      </ul>
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
    position: absolute;
    height: 100%;
    left: 0;
    bottom: 0;
    overflow-y: scroll;
  }

  .province ul,.city ul,.district ul{
    display: flex;
    flex-direction: column;
  }

  .province ul li,.city ul li,.district ul li{
    float: none;
  }

  .province ul li .txt,.city ul li .txt,.district ul li .txt{
    font-size: 1rem;
    display: inline-block;
    padding: 10px 0;
  }

  .city{
    position: absolute;
    height: 100%;
    left: 33.3333%;
    bottom: 0;
    overflow-y: scroll;
  }
  .district{
    position: absolute;
    height: 100%;
    left: 66.6666%;
    bottom: 0;
    overflow-y: scroll;
  }
</style>
