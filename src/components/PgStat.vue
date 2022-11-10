<template>

    <div class="main" id="#sfondo" v-if="pg !== ''">
        <h1>{{ pg }}</h1>

        <div>
            <div v-if="classe === 0">
                <h4>Stama iniziale: <br> <input type="text" v-model="stama" @keyup="stamante()"></h4>
                <h4>Fatica iniziale: <br> <input type="text" v-model="fatica" @keyup="faticante()"></h4>
                <h4>Stama regen: <br> <input type="number" v-model="regenStama"></h4>
                <h4>Fatica regen: <br> <input type="text" v-model="regenFatica"></h4>
                <EnergiaMagica @search="magia" :magia="magiaIniziale"  v-if="pg ==='Mago' "/>

            </div>
            <div class="button__top">
                <button @click="vedi()">{{ dati }} </button>
                <button v-if="classe === 1" @click="nuovoCombat()">Nuovo Combat </button>
            </div>

        </div>

        <div v-if="classe === 1">
            <p>Stama attuale :{{ stamaAttuale }} <span>\Regen: {{ regenStama }}</span> </p>
            <p>Fatica attuale: {{ faticaAttuale }} <span>\Regen: {{ regenFatica }}</span> </p>
          {{magiaIniziale}}
            <StatMagica v-if="pg ==='Mago' " />
            <div class="button">

                <button class="inizio__turno" @click="inizioTurno()">Inizio Turno</button>
                <button @click="attaccoLeggero()">Attacco Leggero</button>
                <button class="secondari" @click="abilitaLeggera()">Abilità Leggera</button>
                <button @click="attaccoPesante()">Attacco Pesante</button>
                <button class="secondari" @click="abilitaPesante()">Abilità Pesante</button>
                <button @click="azioneDifensiva()">Azione Difensiva</button>
                <BottoneMagica v-if="pg ==='Mago' " />
                <button class="fine__turno" @click="fineTurno()">Fine Turno</button>
                <button class="fine__turno" @click="nessunaAzione()">Nessuna Azione</button>
            </div>
        </div>
        <div> <button @click="cambioSfondo()">prova_cambio_img</button></div>


    </div>
</template>

<script>
import EnergiaMagica from './EnergiaMagica.vue';
import StatMagica from './StatMagica.vue';
import BottoneMagica from './BottoneMagica.vue';

export default {
    props: {
        pg: String
    },
    data() {
        return {
            stama: 0,
            fatica: 0,
            stamaAttuale: "",
            magiaIniziale:'',
            cambioStama: "",
            regenStama: 10,
            regenFatica: 1,
            cambioFatica: "",
            faticaAttuale: "",
            azioniDifensive: 1,
            classe: 0,
            dati: "Inserisci i tuoi dati",
            contaSfondo: 0
        };
    },
    // computed: {
    // cambioStama: function () {
    //     console.log("ciao");
    //     return this.stama;
    // }
    // },
    methods: {
        magia(data) {
            console.log(data)
            this.magiaIniziale = data
        },
        nuovoCombat() {
            this.stamante();
            this.faticante();
        },
        stamante() {
            this.cambioStama = this.stama;
            this.stamaAttuale = this.cambioStama;
        },
        faticante() {
            this.cambioFatica = this.fatica;
            this.faticaAttuale = this.cambioFatica;
        },
        attaccoLeggero() {
            // console.log(this.stamaAttuale)
            this.stamaAttuale = this.cambioStama;
            this.stamaAttuale = this.stamaAttuale - 10;
            this.cambioStama = this.stamaAttuale;
            this.faticaAttuale = this.cambioFatica;
            this.faticaAttuale = this.faticaAttuale - 2;
            this.cambioFatica = this.faticaAttuale;
        },
        abilitaLeggera() {
            // console.log(this.stamaAttuale)
            this.stamaAttuale = this.cambioStama;
            this.stamaAttuale = this.stamaAttuale - 2;
            this.cambioStama = this.stamaAttuale;
            this.faticaAttuale = this.cambioFatica;
            this.faticaAttuale = this.faticaAttuale - 1;
            this.cambioFatica = this.faticaAttuale;
        },
        attaccoPesante() {
            // console.log(this.stamaAttuale)
            this.stamaAttuale = this.cambioStama;
            this.stamaAttuale = this.stamaAttuale - 15;
            this.cambioStama = this.stamaAttuale;
            this.faticaAttuale = this.cambioFatica;
            this.faticaAttuale = this.faticaAttuale - 3;
            this.cambioFatica = this.faticaAttuale;
        },
        abilitaPesante() {
            // console.log(this.stamaAttuale)
            this.stamaAttuale = this.cambioStama;
            this.stamaAttuale = this.stamaAttuale - 4;
            this.cambioStama = this.stamaAttuale;
            this.faticaAttuale = this.cambioFatica;
            this.faticaAttuale = this.faticaAttuale - 2;
            this.cambioFatica = this.faticaAttuale;
        },
        azioneDifensiva() {
            // console.log(this.stamaAttuale)
            this.stamaAttuale = this.cambioStama;
            this.stamaAttuale = this.stamaAttuale - (this.azioniDifensive * 5);
            this.cambioStama = this.stamaAttuale;
            this.azioniDifensive++;
        },
        fineTurno() {
            this.regenDiTurno(0, 0);
            // this.stamaAttuale = this.cambioStama
            // this.stamaAttuale = parseInt(this.stamaAttuale) + parseInt(this.regenStama)
            // this.cambioStama = this.stamaAttuale
            // this.faticaAttuale = this.cambioFatica
            // this.faticaAttuale = parseInt(this.faticaAttuale) + parseInt(this.regenFatica)
            // this.cambioFatica = this.faticaAttuale
        },
        nessunaAzione() {
            // this.stamaAttuale = this.cambioStama
            // this.stamaAttuale = parseInt(this.stamaAttuale) + parseInt(this.regenStama) +5
            // this.cambioStama = this.stamaAttuale
            // this.faticaAttuale = this.cambioFatica
            // this.faticaAttuale = parseInt(this.faticaAttuale) + parseInt(this.regenFatica) +1
            // this.cambioFatica = this.faticaAttuale
            this.regenDiTurno(5, 1);
        },
        regenDiTurno(x, y) {
            this.stamaAttuale = this.cambioStama;
            this.stamaAttuale = parseInt(this.stamaAttuale) + parseInt(this.regenStama) + x;
            if (this.stamaAttuale > this.stama) {
                this.stamaAttuale = this.stama;
            }
            this.cambioStama = this.stamaAttuale;
            this.faticaAttuale = this.cambioFatica;
            this.faticaAttuale = parseInt(this.faticaAttuale) + parseInt(this.regenFatica) + y;
            if (this.faticaAttuale > this.fatica) {
                this.faticaAttuale = this.fatica;
            }
            this.cambioFatica = this.faticaAttuale;
        },
        inizioTurno() {
            this.azioniDifensive = 1;
        },
        cambioSfondo() {
            let sfondo = document.getElementById("#sfondo");
            console.log(sfondo);
            if (this.contaSfondo === 0 && this.pg==='Guerriero') {
                sfondo.style.backgroundImage = "url(" + require("../assets/guerriero_liv_1-10pergamena.jpg") + ")";
                this.contaSfondo++;
            }
            else if(this.pg==='Guerriero') {
                
                sfondo.style.backgroundImage = "url(" + require("../assets/warliv10.jpeg") + ")";
                this.contaSfondo = 0;
            }
            else if(this.pg!=='Guerriero') {
                sfondo.style.backgroundImage = "url(" + require("../assets/sfondo-di-carta-grunge_1048-10849.jpg") + ")";
                this.contaSfondo = 0;
            }
        },
        vedi() {
            if (this.classe === 0) {
                this.classe = 1;
                this.dati = "Hai sbagliato i tuoi dati?";
            }
            else {
                this.classe = 0;
                this.dati = "inserisci i tuoi dati";
            }
        }
    },
    components: { EnergiaMagica, StatMagica, BottoneMagica },

}


</script>

<style scoped lang="scss">
.main {

    // background-image: url(../assets/guerriero_liv_1-10pergamena.jpg);
    background-image: url(../assets/sfondo-di-carta-grunge_1048-10849.jpg) ;
    background-size: cover;
    background-repeat: no-repeat;
    // background-position: 0px -50px;
    background-color: white;
    height: 80%;
    border: 1px solid black;
    border-radius: 25px;
    overflow: hidden;
    text-align: start;
    padding: 0px 5px;


    h4,p,h1 {
        padding: 5px;
    }

  

    .button__top {
        display: flex;
        gap: 5px;
        padding-top: 5px;

        button {
            background: rgb(2, 0, 36);
            background: linear-gradient(18deg, rgba(2, 0, 36, 1) 0%, rgba(53, 214, 136, 1) 55%, rgba(0, 212, 255, 1) 100%);
            padding: 0 25px;
            border-radius: 15px;
            color: white;
            min-height: 35px;

        }
    }

    .button {
        display: flex;
        gap: 5px;
        flex-direction: column;
        justify-content: center;
        align-items: flex-start;
        padding-top: 15px;


        button {
            background-color: lightcoral;
            padding: 0 25px;
            border-radius: 15px;
            width: 100px;

            &:hover {
                background-color: cyan;
            }

        }

        .secondari {
            background-color: lemonchiffon;
        }

        .fine__turno {
            background-color: red;
        }

        .inizio__turno {
            background-color: sandybrown;
        }
    }

    span {
        color: green;
        font-weight: 900;
    }
}
</style>