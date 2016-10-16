<template>
  <div class="container">
    <div class="row text-center">
      <div class="col-md-12">
        <h1> vue城市级联选择 </h1>
      </div>
    </div>
    <div class="row">
      <div class="col-md-4 col-md-offset-4">
        <cascading-address @confirm="confirmCity" input-class="input-sm"></cascading-address>
      </div>

    </div>
    <div class="row">
      <div class="col-md-4 col-md-offset-4">
        <pre>{{ confirmData || 'confirm事件中的data将显示在此处' }}</pre>
      </div>
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
      }
    }
  }
</script>

<style>

</style>
