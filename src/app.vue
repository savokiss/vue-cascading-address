<template>
  <div class="demo-container">
    <h1> vue城市级联选择 </h1>
    <cascading-address @confirm="confirmCity"
                       input-class="input-sm"></cascading-address>

    <pre>{{ confirmData || 'confirm事件中的data将显示在此处' }}</pre>
  </div>
  </div>
</template>

<script lang="babel">
  import cascadingAddress from './cascadingAddress'
  export default {
    data(){
      return {
        confirmData : ''
      }
    },
    components: {
      cascadingAddress
    },
    methods: {
      confirmCity(data){
        this.confirmData = data;
        console.log('This is new')
      }
    }
  }
</script>

<style>
.demo-container {
  width: 300px;
  margin: 0 auto;
}

.text-center {
  text-align: center;
}
</style>
