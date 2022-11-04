<template>
  <div class="background">
    <div class="container">
      <h1>Disegni fatti da quello stronzo di Murdock</h1>
      <p>
        Scegli la tua classe:
        <select name="weew" id="" v-model="classe" >
          <option value=""></option>
          <option value="Guerriero">Guerriero</option>
          <option value="Berseker">Berseker</option>
          <option value="Ladro">Ladro</option>
          <option value="Ramingo">Ramingo</option>
          <option value="Druido">Druido</option>
          <option value="Mago">Mago</option>
          <option value="Chierico">Chierico</option>
          <option value="Guardiano">Guardiano</option>
        </select>
      </p>
      <p>La tua classe è {{classe}} </p>
      <p>{{cambioClasse}}</p>
      <GuerrieroStat v-if="classe==='Guerriero'"/>
    </div>
  </div>
</template>

<script>
import GuerrieroStat from "./GuerrieroStat.vue";
export default {
    data() {
        return {
            classe: ""
        };
    },
    methods:{
      

    },
    computed: {
        cambioClasse: function () {
            console.log("ciao");
            return this.classe;
        }
    },
    components: { GuerrieroStat }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.background {
  background-color: bisque;
  height: 100%;

  .container {
    max-width: 320px;
    margin: 0 auto;
    background-color: #e4bf8a;
    border: 1px solid black;
    border-radius: 15px;
    height: 100%;
    text-align: center;
  
  }
}
</style>
