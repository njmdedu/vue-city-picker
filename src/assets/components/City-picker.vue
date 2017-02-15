<template lang="html">
  <div class="root">
    <div class="col province">
      <ul>
        <li v-for="province in provinces" @click="selectCitysByProvinceCode(province.code)">
          <span class="txt">{{province.name}}</span>
        </li>
      </ul>
    </div>
    <div class="col city" >
      <ul>
        <li v-for="city in citys" @click="selectDistrictsByCityCode(city.code)">
          <span class="txt">{{city.name}}</span>
        </li>
      </ul>
    </div>
    <div class="col district">
      <ul>
        <li v-for="district in districts">
          <span class="txt">{{district.name}}</span>
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
            citydata: citydata.citydata,
            provinces:[{
              name:'请选择'
            }],
            citys:[{
              name:'请选择'
            }],
            districts:[{
              name:'请选择'
            }]
        }
    },
    created(){
      var that = this;
      $.each(that.citydata, function(index, obj) {
          that.provinces.push({
              name: obj.name,
              code: obj.code,
              sub: obj.sub
          });
      });
    },
    methods: {
        selectCitysByProvinceCode(code) {
          let that = this;
          $.each(that.provinces,function(index, obj){
                if(obj.code === code){
                  $.each(obj.sub,function(i,o){
                    that.citys.push({
                      name : o.name,
                      code : o.code,
                      sub : o.sub
                    });
                  })
                  return false;
                }
              });
        },
        selectDistrictsByCityCode(code) {
          let that = this;
          $.each(that.citys,function(index, obj){
               if(obj.code === code){
                 $.each(obj.sub,function(i,o){
                   that.districts.push({
                     name : o.name,
                     code : o.code,
                     sub : o.sub
                   });
                 })
                 return false;
               }
             });
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
    overflow: hidden;
    text-overflow: ellipsis;
    display: inline-block;
    white-space: nowrap;
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
