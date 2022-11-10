<template>
    <div>
    <h1>BOTTONE</h1>
    <button @click="provamana()"> Prova scala mana</button>
    </div>
   </template>
   
   <script> 
  
   
   export default {
    data() {
        return {
          
        };
    },
    methods:{
        provamana(){
            console.log(this.stama)
        }

    },
    
      
   }
   </script>
   
   <style lang="scss" scoped>
  h1{
    color: white
  }
   </style>
   