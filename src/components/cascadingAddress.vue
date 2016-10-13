<template>
  <div>
    <input v-model="all" @click="open('show')" type="text" class="form-control"
           :class="{submmited : !p }" readonly="true"/>

    <div v-show="show" class="cascading-address">
      <ul>
        <li v-for="item in provinces" @click="setProvince(item.p)" :class="{'label label-success': p === item.p}">
          {{ item.p }}
        </li>
      </ul>

      <ul v-show="cities.length">
        <li v-for="item in cities" @click="setCity(item.n)" :class="{'label label-success': c === item.n}">
          {{ item.n }}
        </li>
      </ul>

      <ul v-show="dists.length">
        <li v-for="item in dists" @click="setArea(item.s)" :class="{'label label-success': a === item.s}">
          {{ item.s }}
        </li>
      </ul>

      <div v-show="p" class="form-group text-left">
        <label class="control-label text-success">
          <span class="text-muted">地址：</span>
          {{ p }} {{ c }} {{ a }} {{ d }}
          <!--{{ p }} {{ c }}-->
        </label>
      </div>

      <div class="panel-footer text-right">
        <button @click="clear()" class="btn btn-link btn-sm">清空</button>
        <button @click="confirm()" class="btn btn-success btn-sm" :disabled="!(p&&c) && p!='国外'">确定</button>
      </div>
    </div>
  </div>
</template>
<style>
  .cascading-address {
    box-shadow: 0 6px 12px rgba(0, 0, 0, .175);
    position: absolute;
    z-index: 99999;
    background: #fff;
    width: 318px;
  }

  .cascading-address ul {
    padding: 5px;
    border-bottom: 1px dotted #ddd;
    text-align: left;
  }

  .cascading-address ul li {
    font-size: 13px;
    list-style: none;
    display: inline-block;
    margin: 5px 7px;
    cursor: pointer;
  }

  .cascading-address .form-group {
    margin: 10px;
  }

  .input.error {
    border: solid 1px #a94442;
  }

  .text-danger {
    position: relative;
    left: -2px;
  }
</style>
<script lang="babel">
  import addressData from './cascadingAddressData.json'
  export default{
    data(){
      return {
        all: '',
        p: '',
        c: '',
        a: '',
        d: '',
        provinces: addressData,
        dists: '',
        cities: '',
        show: false,
        set: ''
      }
    },
    methods: {
      init(){
        // 根据选中的 p(省份) 值更新 cities(城市列表)
        this.$watch('p', function (newValue) {
          if(newValue) {
            var result = this.provinces.filter(function (v) {
              return v.p === newValue;
            });
            this.cities = result[0].c;
          } else {
            this.cities = [];
          }
        }).bind(this)

        // 类似以上
        this.$watch('c', function (newValue) {
          if(newValue) {
            var result = this.cities.filter(function (v) {
              return v.n === newValue;
            });
            this.dists = result[0].a;
          } else {
            this.dists = [];
          }
        }).bind(this)

        // 任何数据变动都更新完整地址
        this.$watch(function () {
          var address = (this.p + ' ' + this.c + ' ' + this.a + ' ' + this.d);
          this.all = address.replace(/undefined *|   /g,'');
        }).bind(this)
      },
      clear(){
        this.p = '';
        this.c = '';
        this.a = '';
        this.d = '';
      },
      open(action){
        this.show = action === 'show';
      },
      confirm(){
        this.show = false;
      },
      setProvince(p){
        this.p = p;
        this.c = '';
        this.a = '';
        this.d = '';
      },
      setCity(c){
        this.c = c;
        this.a = '';
        this.d = '';
      },
      setArea(a){
        this.a = a;
        this.d = '';
      }
    },
    mounted(){
      this.init();
    }
  }
</script>
