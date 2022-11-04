<template>
  <div id="app">
    <MainBody/>
  </div>
</template>

<script> 
import MainBody from './components/MainBody.vue';


export default {
    components: { MainBody },
   
}
</script>

<style lang="scss">
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
#app{
  height: 100vh;
}
</style>
