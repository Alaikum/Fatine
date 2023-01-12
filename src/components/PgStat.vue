<template>

    <div class="main" v-if="pg !== ''">
        <h1>{{ pg }} <span @click="settingMenu()" class="setting" v-if="classe === 1"><font-awesome-icon
                    icon="fa-solid fa-gears" v-if="!setting" /></span>
        </h1>
        <div class="menu__setting" v-if="setting">

            <h1 class="title__setting">{{ pg }} <span @click="settingMenu()" class="setting"
                    v-if="classe === 1"><font-awesome-icon icon="fa-solid fa-xmark" /></span>

            </h1>
            <ul class="ul__setting">
                <li :class="settingAttLeg ? '' : 'setting__off'" @click="setAttLeg()">Attacco Leggero</li>
                <li :class="settingAbiLeg ? '' : 'setting__off'" @click="setAbiLeg()">Abilità Leggera</li>
                <li :class="settingAttPes ? '' : 'setting__off'" @click="setAttPes()">Attacco Pesante</li>
                <li :class="settingAbiPes ? '' : 'setting__off'" @click="setAbiPes()">Abilità Pesante</li>
                <li :class="settingAziDif ? '' : 'setting__off'" @click="setAziDif()">Azione Difensiva</li>
                <li :class="settingConMag ? '' : 'setting__off'" @click="setConMag()" v-if="classeMagica()">Consuma
                    Magica</li>
                <li :class="settingConExt ? '' : 'setting__off'" @click="setConExt()">Consumi Extra </li>
                <li class="special" :class="settingConSta ? '' : 'setting__off'" @click="setConSta()">Consuma Stamina
                </li>
                <li class="special" :class="settingConFat ? '' : 'setting__off'" @click="setConFat()">Consume Fatica
                </li>
                <li v-if="classeChierico()" :class="settingLuceBuio ? '' : 'setting__off'" @click="setBuLu()">Luce Buio
                </li>

            </ul>

        </div>
        <div>

            <div v-if="classe === 0">
                <h4>Stama iniziale: <br> <input type="text" v-model="stama" @keyup="stamante()"></h4>
                <h4>Fatica iniziale: <br> <input type="text" v-model="fatica" @keyup="faticante()"></h4>
                <h4>Stama regen: <br> <input type="text" v-model="regenStama"></h4>
                <h4>Fatica regen: <br> <input type="text" v-model="regenFatica"></h4>
                <div v-if="classeMagica()">
                    <h4>Energia Magica Iniziale: <br> <input type="text" v-model="magica" @keyup="magicante()"> </h4>
                    <h4>Magica regen: <br> <input type="text" v-model="regenMagica"></h4>
                </div>
                <div v-if="classeChierico()">
                    <h4>Luce Iniziale: <br> <input type="text" v-model="luce"> </h4>
                    <h4>Buio Iniziale: <br> <input type="text" v-model="buio"></h4>
                    <h4 v-if="parseInt(buio) + parseInt(luce) > 100"
                        style="color:red; background:white; border:1px solid black;">Luce e Buio inseriti in modo errato
                    </h4>
                </div>

            </div>
            <div class="button__top">
                <button @click="vedi()">{{ dati }} </button>
                <button v-if="classe === 1" @click="nuovoCombat()">Nuovo Combat </button>
            </div>

        </div>

        <div v-if="classe === 1">
            <p>Stama attuale :{{ stamaAttuale }} <span>\Regen: {{ regenStama }}(+5)</span> </p>
            <p>Fatica attuale: {{ faticaAttuale }} <span>\Regen: {{ regenFatica }}(+1)</span> </p>
            <p v-if="classeMagica()">Energia Magica attuale: {{ magicaAttuale }} <span>\Regen: {{
                regenMagica
            }}(+1)</span> </p>

            <div class="main__button" id="#sfondo">

                <div class="button">

                    <button class="inizio__turno" @click="inizioTurno()">{{ inizio }}</button>
                    <button @click="attaccoLeggero()" v-if="settingAttLeg">Attacco Leggero</button>
                    <button class="secondari" @click="abilitaLeggera()" v-if="settingAbiLeg">Abilità Leggera</button>
                    <button @click="attaccoPesante()" v-if="settingAttPes">Attacco Pesante</button>
                    <button class="secondari" @click="abilitaPesante()" v-if="settingAbiPes">Abilità Pesante</button>
                    <button @click="azioneDifensiva()" v-if="settingAziDif">Azione Difensiva</button>
                    <div class="" v-if="classeMagica() && settingConMag">
                        <h4 class="text__out__button">Inserisci qui il consumo di energia Magica:</h4>
                        <div class="consumi">
                            <input class="consumi__input" type="text" v-model="consumoMagia">
                            <button @click="consumoMagica()"> Consuma Magica</button>
                        </div>
                    </div>
                    <div class="arrow" @click="consumiExtra()" v-if="settingConExt">
                        <button class="secondari"> Consumi Extra </button>
                        <strong v-if="!consumi">&DownArrowBar;</strong>
                        <strong v-if="consumi">&UpArrowBar;</strong>
                    </div>
                    <div class="" v-if="consumi">
                        <div v-if="settingConSta">
                            <h4 class="text__out__button">Inserisci qui il consumo di Stamina Extra:</h4>
                            <div class="consumi">
                                <input class="consumi__input" type="text" v-model="consumoSta">
                                <button @click="consumoStamina()"> Consuma Stamina</button>
                            </div>
                        </div>
                        <div v-if="settingConFat">
                            <h4 class="text__out__button">Inserisci qui il consumo di Fatica Extra:</h4>
                            <div class="consumi">
                                <input class="consumi__input" type="text" v-model="consumoFat">
                                <button @click="consumoFatica()"> Consuma Fatica</button>
                            </div>
                        </div>
                    </div>
                    <button class="fine__turno" @click="fineTurno()">Fine Turno</button>
                    <button class="fine__turno" @click="nessunaAzione()">Nessuna Azione</button>
                    <button @click="cambioSfondo()">prova cambio img</button>
                    <figure v-if="classeChierico() && settingLuceBuio" class="container__luce_buio">
                        <img class="luce_buio" src="../assets/tao.jpeg" alt="">
                        <h4 class="luce" @click="addLuce()">{{ luce }}</h4>
                        <h4 class="buio" @click="addBuio()">{{ buio }}</h4>
                    </figure>
                </div>

            </div>
        </div>

    </div>
</template>

<script>


export default {
    props: {
        pg: String
    },
    data() {
        return {
            stama: 0,
            fatica: 0,
            magica: 0,
            stamaAttuale: "",
            cambioStama: "",
            regenStama: 10,
            consumoSta: 0,
            regenFatica: 1,
            regenMagica: 0,
            cambioFatica: "",
            faticaAttuale: "",
            consumoFat: 0,
            azioniDifensive: 1,
            magicaAttuale: "",
            cambioMagica: "",
            consumoMagia: 0,
            classe: 0,
            dati: "Inserisci i tuoi dati",
            contaSfondo: 0,
            consumi: false,
            inizio: 'Inizio Combat',
            combattimento: false,
            setting: false,
            settingAttLeg: true,
            settingAbiLeg: true,
            settingAttPes: true,
            settingAbiPes: true,
            settingAziDif: true,
            settingConMag: true,
            settingConExt: true,
            settingConSta: true,
            settingConFat: true,
            settingLuceBuio: true,
            luce: 0,
            buio: 0

        };
    },
    // computed: {
    // cambioStama: function () {
    //     console.log("ciao");
    //     return this.stama;
    // }
    // },
    watch: {
        stamaAttuale() {
            if (this.stamaAttuale < 1 && this.combattimento) alert('STAMA FINITA')

        },
        faticaAttuale() {
            if (this.faticaAttuale < 1 && this.combattimento) alert('FATICA FINITA')

        },
        magicaAttuale() {
            if (this.classeMagica()) {
                if (this.magicaAttuale < 1 && this.combattimento) alert('ENERGIA MAGICA FINITA')
            }

        },
        luce(newLuce) {
            localStorage.luce = newLuce;
        },
        buio(newBuio) {
            localStorage.buio = newBuio;
        }


    },
    mounted() {
        if (localStorage.luce) {
            this.luce = localStorage.luce;
        }
        if (localStorage.buio) {
            this.buio = localStorage.buio;
        }
    },
    methods: {
        settingMenu() {
            this.setting = !this.setting
        },
        setAttLeg() {
            this.settingAttLeg = !this.settingAttLeg
        },
        setAbiLeg() {
            this.settingAbiLeg = !this.settingAbiLeg
        },
        setAttPes() {
            this.settingAttPes = !this.settingAttPes
        },
        setAbiPes() {
            this.settingAbiPes = !this.settingAbiPes
        },
        setAziDif() {
            this.settingAziDif = !this.settingAziDif
        },
        setConMag() {
            this.settingConMag = !this.settingConMag
        },
        setConExt() {
            this.settingConExt = !this.settingConExt
        },
        setConSta() {
            this.settingConSta = !this.settingConSta
        },
        setConFat() {
            this.settingConFat = !this.settingConFat
        },
        setBuLu() {
            this.settingLuceBuio = !this.settingLuceBuio
        },

        nuovoCombat() {
            this.stamante();
            this.faticante();
            this.magicante();
            this.inizio = 'Inizio Combat';

        },
        consumiExtra() {
            this.consumi = !this.consumi
        },
        stamante() {
            this.cambioStama = this.stama;
            this.stamaAttuale = this.cambioStama;
        },
        faticante() {
            this.cambioFatica = this.fatica;
            this.faticaAttuale = this.cambioFatica;
        },
        magicante() {
            this.cambioMagica = this.magica;
            this.magicaAttuale = this.cambioMagica;
        },
        consumoStamina() {
            this.stamaAttuale = this.cambioStama;
            this.stamaAttuale = this.stamaAttuale - this.consumoSta;
            this.cambioStama = this.stamaAttuale;

        },
        consumoFatica() {
            this.faticaAttuale = this.cambioFatica;
            this.faticaAttuale = this.faticaAttuale - this.consumoFat;
            this.cambioFatica = this.faticaAttuale;
        },
        consumoMagica() {
            this.magicaAttuale = this.cambioMagica;
            this.magicaAttuale = this.magicaAttuale - this.consumoMagia;
            this.cambioMagica = this.magicaAttuale;
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
            this.regenDiTurno(0, 0, 0);
        },
        nessunaAzione() {
            this.regenDiTurno(5, 1, 1);
        },
        regenDiTurno(x, y, z) {
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

            this.magicaAttuale = this.cambioMagica;
            this.magicaAttuale = parseInt(this.magicaAttuale) + parseInt(this.regenMagica) + z;
            if (this.magicaAttuale > this.magica) {
                this.magicaAttuale = this.magica;
            }
            this.cambioMagica = this.magicaAttuale;

        },
        inizioTurno() {
            this.azioniDifensive = 1;
            this.inizio = 'Inizio Turno';

        },
        cambioSfondo() {
            let sfondo = document.getElementById("#sfondo");
            console.log(sfondo);
            if (this.contaSfondo === 0 && this.pg === 'Guerriero') {
                sfondo.style.backgroundImage = "url(" + require("../assets/guerriero_liv_1-10pergamena.jpg") + ")";
                this.contaSfondo++;
            }
            else if (this.pg === 'Guerriero') {

                sfondo.style.backgroundImage = "url(" + require("../assets/warliv10.jpeg") + ")";
                this.contaSfondo = 0;
            }
            else if (this.pg !== 'Guerriero') {

                if (this.contaSfondo === 0 && this.pg === 'Mago') {
                    sfondo.style.backgroundImage = "url(" + require("../assets/maga_liv1-10.jpg") + ")";
                    this.contaSfondo++;

                } else {
                    sfondo.style.backgroundImage = "url(" + require("../assets/sfondo-di-carta-grunge_1048-10849.jpg") + ")";
                    this.contaSfondo = 0;
                }

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
            this.combattimento = !this.combattimento
        },
        classeMagica() {
            let p = this.pg
            if (p === 'Mago' || p === 'Chierico' || p === 'Druido' || p === 'Guardiano') {
                return true
            }
            return false
        },
        classeChierico() {
            let p = this.pg
            if (p === 'Chierico') {
                return true
            }
            return false
        },
        addLuce() {
            this.luce++
            if (parseInt(this.buio) + parseInt(this.luce) > 100) {
                let l = this.luce
                let b = this.buio
                if (l > 100) {
                    this.luce = 100
                    return
                }
                b = parseInt(b) - (parseInt(l) + parseInt(b) - 100)
                this.buio = b
            }
        },
        addBuio() {
            this.buio++
            if (parseInt(this.buio) + parseInt(this.luce) > 100) {
                let l = this.luce
                let b = this.buio
                if (b > 100) {
                    this.buio = 100
                    return
                }
                l = parseInt(l) - (parseInt(l) + parseInt(b) - 100)
                this.luce = l
            }
        }
    },


}


</script>

<style scoped lang="scss">
.container__luce_buio {
    max-width: 50%;
    position: relative;


    .luce_buio {
        max-width: 100%;
        border-radius: 25px;
    }

    .luce,
    .buio {
        position: absolute;
        border: 1px dashed currentColor;
        padding: 1rem;
        font-size: 2rem;
        border-radius: 25px;
        cursor: pointer;
    }

    .luce {
        color: white;
        top: 0;
        left: 0;

    }

    .buio {
        color: black;
        bottom: 0;
        right: 0;

    }
}

.main {

    // background-image: url(../assets/guerriero_liv_1-10pergamena.jpg);
    // background-image: url(../assets/sfondo-di-carta-grunge_1048-10849.jpg);
    background-size: cover;
    background-repeat: no-repeat;
    background-position: center center;
    // border: 1px solid black;
    border-radius: 25px;
    overflow: hidden;
    text-align: start;
    padding: 10px 5px;
    position: relative;


    h4,
    p,
    h1 {
        padding: 5px;

    }


    .setting {
        color: black;
        position: relative;
        left: 25px;

        &:hover {
            color: white;
            border: 1px solid black;
            cursor: pointer;
        }
    }

    .menu__setting {
        position: absolute;
        top: 0;
        bottom: 0;
        right: 0;
        left: 0;
        background-color: rgba(0, 0, 0, 0.5);
        padding: 10px 5px;
    }

    .title__setting {
        display: flex;
        flex-direction: row;
        color: white;

        .setting {
            color: white;
        }

    }

    .ul__setting {
        color: white;
        text-align: center;
        padding: 1rem;
        list-style: none;
        display: flex;
        flex-direction: column;
        gap: 5px;
        justify-content: flex-end;
        align-items: flex-end;



        li {
            padding: 1rem;
            border: 1px solid black;
            max-width: 200px;
            border-radius: 15px;
            background-color: green;

            &:hover {
                cursor: pointer;
            }
        }

        .special {
            background-color: sandybrown;
        }

        .setting__off {
            background-color: red;
            color: black;
        }
    }

    .text__out__button {
        color: black;
        background-color: rgba(230, 210, 200, 0.7);
    }

    .main__button {

        // justify-content: space-between;
        // background-image: url(../assets/maga_liv1-10.jpg);
        background-size: cover;
        background-repeat: no-repeat;
        // background-position: center center;
        border: 1px solid black;
        border-radius: 25px;
        overflow: hidden;


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
        min-height: 400px;


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

    .consumi {
        display: flex;
        justify-content: space-between;
    }

    .consumi__input {
        border-radius: 10px;
        padding: 5px;
    }

    .arrow {
        display: flex;
        justify-content: center;
        align-items: center;
        gap: 15px;

        strong {
            font-size: 1.5rem;
            border: 1px solid black;
            padding: 5px;
            border-radius: 10px;
            background-color: lemonchiffon;


        }
    }
}
</style>