<template>
  <div class="container">
    <div class="row text-center">
      <div class="col-md-12">
        <h1> 本系统中提供的所有可转换汉字列表</h1>
      </div>
    </div>
    <div class="row">
      <form name="transferForm" class="form-horizontal">
        <div class="form-group text-center">
          <div class="col-md-3 col-md-offset-3">
            <input class="form-control" v-model="searchKey" placeholder="请输入汉字" v-change="toUnicode(searchKey)">
          </div>
          <div class="col-md-3">
            <input class="form-control" v-model="unicode" placeholder="这里为汉字对应的unicode码">
          </div>
        </div>
      </form>
    </div>
    <div class="row">  
      <div class="col-md-10 col-md-offset-1">
        <table class="table table-striped table-hover">
          <thead>
            <tr>
              <th>拼音</th>
              <th>汉字</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="item in filteredList">
              <td>{{ item.key }}</td>
              <td>{{ item.value }}</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
  import pinyin from './pinyin.json'
  export default {
    data() {
      return {
        unicode: '',
        word: '',
        searchKey: '',
        pinyinDict: pinyin.full_dict
      }
    },
    computed: {
      pinyinList() {
        var res = [];
        Object.keys(this.pinyinDict).forEach(v => res.push({
          key: v,
          value: this.pinyinDict[v]
        }))
        return res;
      },
      filteredList() {
        return this.pinyinList.filter((item) => {
          return item.key.indexOf(this.searchKey) !== -1 || item.value.indexOf(this.searchKey) !== -1
        })
      }
    },
    methods: {
      toUnicode(word) {
        return this.unicode = escape(word).toLocaleLowerCase().replace(/%u/gi, '\\u');
      },
      toChinese(unicode) {
        return unescape(unicode.replace(/\u/g, '%u'));
      }
    },
    mounted() {

    }
  }
</script>

<style>

</style>