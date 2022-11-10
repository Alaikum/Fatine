<template>
    <div>
        <h1>inserisci mana</h1>
        <h1>

          
        </h1>
        <h4>Energia Magica Iniziale: <br> <input type="text" v-model="magiaIniziale"
                @change="$emit('search', magiaIniziale)" :placeholder=this.magia ></h4>
    </div>
</template>
   
<script>


export default {
    props: {
        magia: String
    },
    data() {
        return {
            magiaIniziale: '',
            

        };
    },
    methods:{
      
    },

}
</script>
   
<style lang="scss" scoped>
h1 {
    color: white
}
</style>
   