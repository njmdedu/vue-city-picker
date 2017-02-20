<template lang="html">
  <div class="root">
    <div class="col province">
      <ul>
        <li v-bind:data-code="province.code" v-bind:class="{active:activeProvince.code == province.code}" v-for="province in provinces" @click="selectCitysByProvinceCode(province)">
          <span class="txt">{{province.name}}</span>
        </li>
      </ul>
    </div>
    <div class="col city" >
      <ul>
        <li v-bind:class="{active:activeCity.code == city.code}" v-for="city in citys" @click="selectDistrictsByCityCode(city)">
          <span class="txt">{{city.name}}</span>
        </li>
      </ul>
    </div>
    <div class="col district">
      <ul>
        <li v-bind:class="{active:activeDistrict.code == district.code}" v-for="district in districts" @click="selectDistrict(district)">
          <span class="txt">{{district.name}}</span>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import citydata from './../city-datas'
export default {
    //props: ['msg'],
    data() {
        return {
            citydata: citydata.citydata,
            provinces:[],
            citys:[],
            districts:[],
            activeProvince:{
              name:'',
              code:''
            },
            activeCity:{
              name:'',
              code:''
            },
            activeDistrict:{
              name:'',
              code:''
            }
        }
    },
    created(){
      var that = this;

      that.provinces.push({
        name:'不限',
        code:'0',
        active:false
      })
      $.each(that.citydata, function(index, obj) {
          that.provinces.push({
              name: obj.name,
              code: obj.code,
              sub: obj.sub,
              active:false
          });
      });
    },
    methods: {
        resetCity(){
          this.citys=[];
          this.activeCity={
            name:'',
            code:''
          }
        },
        resetDistrict(){
          this.districts=[];
          this.activeDistrict={
            name:'',
            code:''
          }
        },
        setCodes(){
          var codes = [];
          if (this.activeProvince.code&&this.activeProvince.code!=0) {
            codes.push(this.activeProvince.code);
          }
          if(this.activeCity.code&&this.activeCity.code!=0) {
            codes.push(this.activeCity.code);
          }
          if(this.activeDistrict.code&&this.activeDistrict.code!=0) {
            codes.push(this.activeDistrict.code);
          }
          return codes.join(',');
        },
        selectCitysByProvinceCode(province) {
          let that = this;
          that.activeProvince = province;
          that.resetCity();
          that.resetDistrict();
          that.$emit('setRootCodes',that.setCodes());
          if (province.code==0) {
            that.$emit('closeModal');
            return;
          }
          that.citys.push({
            name:'不限',
            code:'0',
            active:false
          })
          $.each(that.provinces,function(index, obj){
                if(obj.code === province.code){
                  $.each(obj.sub,function(i,o){
                    that.citys.push({
                      name : o.name,
                      code : o.code,
                      sub : o.sub,
                      active:false
                    });
                  })
                  return false;
                }
              });
        },
        selectDistrictsByCityCode(city) {
          let that = this;
          that.resetDistrict();
          that.activeCity=city;
          that.$emit('setRootCodes',that.setCodes());
          if (city.code==0) {
            that.$emit('closeModal');
            return;
          }
          that.districts.push({
            name:'不限',
            code:'0',
            active:false
          })
          $.each(that.citys,function(index, obj){
               if(obj.code === city.code){
                 $.each(obj.sub,function(i,o){
                   that.districts.push({
                     name : o.name,
                     code : o.code,
                     sub : o.sub,
                     active:false
                   });
                 })
                 return false;
               }
             });
        },
        selectDistrict(district){
          this.activeDistrict=district;
          this.$emit('setRootCodes',this.setCodes());
          this.$emit('closeModal');
        }
    }
}
</script>

<style lang="css">
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

  .province ul .active,.city ul .active,.district ul .active{
  color:#009E48;
  }
  .province ul li,.city ul li,.district ul li{
    overflow: hidden;
    text-overflow: ellipsis;
    display: inline-block;
    white-space: nowrap;
    padding: 10px;
  }
  .province ul li .txt,.city ul li .txt,.district ul li .txt{
    font-size: 1rem;
  }

  .city{
    position: absolute;
    height: 100%;
    left: 33.3333%;
    bottom: 0;
    overflow-y: scroll;
    border-left: 1px solid #F2F2F3;
  }
  .district{
    position: absolute;
    height: 100%;
    left: 66.6666%;
    bottom: 0;
    overflow-y: scroll;
    border-left: 1px solid #F2F2F3;
  }
</style>
