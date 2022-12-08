<template>
  <div class="background">
    <div class="container">
      <h1 style="padding:1px;">Disegni fatti da quello stronzo di Murdock</h1>
      <p>
        Scegli la tua classe:
        <select name="weew" id="" v-model="classe">
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
      <!-- <p>La tua classe è {{classe}} </p>
      <p>{{cambioClasse}}</p> -->
      <PgStat :pg="classe" />
    </div>
  </div>
</template>

<script>
import PgStat from "./PgStat.vue";
export default {
  data() {
    return {
      classe: ""
    };
  },
  methods: {


  },
  computed: {
    cambioClasse: function () {
      console.log("ciao");
      return this.classe;
    }
  },
  components: { PgStat }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.background {
  background-color: darkolivegreen;
  min-height: 100%;
  // overflow: auto;

  .container {
    max-width: 380px;
    margin: 0 auto;
    // background-color: #e4bf8a;
    background-image: url(../assets/sfondo-di-carta-grunge_1048-10849.jpg);
    box-shadow: 10px 10px 5px #aaaaaa;
    background-repeat: no-repeat;
    background-size: cover;
    border: 1px solid black;
    border-radius: 15px;
    height: 100%;
    text-align: center;

  }
}
</style>
