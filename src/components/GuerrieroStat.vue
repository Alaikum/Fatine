<template>

    <div class="main" id="#sfondo">

        <div>
            <div v-if="classe === 0">
                <h4>Stama iniziale: <input type="text" v-model="stama" @keyup="stamante()"></h4>
                <h4>Fatica iniziale: <input type="text" v-model="fatica" @keyup="faticante()"></h4>
                <h4>Stama regen: <input type="number" v-model="regenStama"></h4>
                <h4>Fatica regen: <input type="text" v-model="regenFatica"></h4>


            </div>
            <button @click="vedi()">{{ dati }} </button>
            
        </div>

        <div v-if="classe === 1">
            <p >Stama attuale :{{ stamaAttuale }} <span>\Regen: {{ regenStama }}</span>   </p>
            <p >Fatica attuale: {{ faticaAttuale }} <span>\Regen: {{ regenFatica }}</span>  </p>
            <div class="button">

                <button class="inizio__turno" @click="inizioTurno()">Inizio Turno</button>
                <button @click="attaccoLeggero()">Attacco Leggero</button>
                <button class="secondari" @click="abilitaLeggera()">Abilità Leggera</button>
                <button @click="attaccoPesante()">Attacco Pesante</button>
                <button class="secondari" @click="abilitaPesante()">Abilità Pesante</button>
                <button @click="azioneDifensiva()">Azione Difensiva</button>
                <button class="fine__turno" @click="fineTurno()">Fine Turno</button>
                <button class="fine__turno" @click="nessunaAzione()">Nessuna Azione</button>
            </div>
        </div>
        <div> <button @click="cambioSfondo()">prova_cambio_img</button></div>


    </div>
</template>

<script>
export default {
    data() {
        return {
            stama: 0,
            fatica: 0,
            stamaAttuale: '',
            cambioStama: '',
            regenStama: 10,
            regenFatica: 1,
            cambioFatica: '',
            faticaAttuale: '',
            azioniDifensive: 1,
            classe: 0,
            dati: 'Inserisci i tuoi dati',
            contaSfondo:0
        }
    },
    // computed: {
    // cambioStama: function () {
    //     console.log("ciao");
    //     return this.stama;
    // }
    // },
    methods: {
        stamante() {
            this.cambioStama = this.stama
            this.stamaAttuale = this.cambioStama
        },
        faticante() {
            this.cambioFatica = this.fatica
            this.faticaAttuale = this.cambioFatica
        },
        attaccoLeggero() {
            // console.log(this.stamaAttuale)
            this.stamaAttuale = this.cambioStama
            this.stamaAttuale = this.stamaAttuale - 10
            this.cambioStama = this.stamaAttuale

            this.faticaAttuale = this.cambioFatica
            this.faticaAttuale = this.faticaAttuale - 2
            this.cambioFatica = this.faticaAttuale

        },
        abilitaLeggera() {
            // console.log(this.stamaAttuale)
            this.stamaAttuale = this.cambioStama
            this.stamaAttuale = this.stamaAttuale - 2
            this.cambioStama = this.stamaAttuale

            this.faticaAttuale = this.cambioFatica
            this.faticaAttuale = this.faticaAttuale - 1
            this.cambioFatica = this.faticaAttuale


        },
        attaccoPesante() {
            // console.log(this.stamaAttuale)
            this.stamaAttuale = this.cambioStama
            this.stamaAttuale = this.stamaAttuale - 15
            this.cambioStama = this.stamaAttuale

            this.faticaAttuale = this.cambioFatica
            this.faticaAttuale = this.faticaAttuale - 3
            this.cambioFatica = this.faticaAttuale

        },
        abilitaPesante() {
            // console.log(this.stamaAttuale)
            this.stamaAttuale = this.cambioStama
            this.stamaAttuale = this.stamaAttuale - 4
            this.cambioStama = this.stamaAttuale

            this.faticaAttuale = this.cambioFatica
            this.faticaAttuale = this.faticaAttuale - 2
            this.cambioFatica = this.faticaAttuale


        },
        azioneDifensiva() {
            // console.log(this.stamaAttuale)
            this.stamaAttuale = this.cambioStama
            this.stamaAttuale = this.stamaAttuale - (this.azioniDifensive * 5)
            this.cambioStama = this.stamaAttuale
            this.azioniDifensive++

        },
        fineTurno() {
            this.stamaAttuale = this.cambioStama
            this.stamaAttuale = parseInt(this.stamaAttuale) + parseInt(this.regenStama)
            this.cambioStama = this.stamaAttuale

            this.faticaAttuale = this.cambioFatica
            this.faticaAttuale = parseInt(this.faticaAttuale) + parseInt(this.regenFatica)
            this.cambioFatica = this.faticaAttuale


        },
        nessunaAzione() {
            this.stamaAttuale = this.cambioStama
            this.stamaAttuale = parseInt(this.stamaAttuale) + parseInt(this.regenStama) +5
            this.cambioStama = this.stamaAttuale

            this.faticaAttuale = this.cambioFatica
            this.faticaAttuale = parseInt(this.faticaAttuale) + parseInt(this.regenFatica) +1
            this.cambioFatica = this.faticaAttuale


        },
        inizioTurno() {
            this.azioniDifensive = 1
        },
        cambioSfondo() {
            let sfondo = document.getElementById('#sfondo');
            console.log(sfondo)
            if (this.contaSfondo===0){
                sfondo.style.backgroundImage = "url(" + require("../assets/warliv10.jpeg") + ")";
                this.contaSfondo++
            }else{
                sfondo.style.backgroundImage = "url(" + require("../assets/war2.jpeg") + ")";
                this.contaSfondo=0
            }

        },
        vedi() {
            if (this.classe === 0) {
                this.classe = 1
                this.dati = 'Hai sbagliato i tuoi dati?'
            } else {
                this.classe = 0
                this.dati = 'inserisci i tuoi dati'
            }
        }

    }
}


</script>

<style scoped lang="scss">
.main {
    background-image: url(../assets/war2.jpeg);
    background-size: contain;
    background-repeat: no-repeat;
    background-position: 65px 75px;
    background-color: white;
    height: 80%;
    overflow: hidden;
    text-align: start;
    padding: 0 5px;

    h4 {
        padding: 5px;
    }

    p {
        padding: 5px;
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
            background-color: green;
        }
    }

    span{
        color: green;
        font-weight: 900;
    }
}
</style>