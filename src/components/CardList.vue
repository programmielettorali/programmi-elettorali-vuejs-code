<template>
        <header class="header">
        <nav>
            <h1 class="title">Programmi 2022</h1>
            <input class="seachbar" type="text" v-model="search" placeholder="&#128269; Cerca!">
        </nav>
    </header>

    <section class="program-list overflow" >
            <div class="card" v-for="party in SearchPartyField" :key="party.id">
                <img :src="require('../assets/Img/' + party.Immagine)" :alt=" party.Nome + ', ' + party.Collocazione">
                <section class="card-content">
                    <h2>{{ party.Nome }}</h2>
                    <p class="tipo">{{ party.Tipo }}</p>
                    <p class="collocazione">Collocazione: <a :href="Collocazionelink(party.Collocazione)" :class="party.Collocazione.toLowerCase()">{{ party.Collocazione }}</a></p>
                    <p class="lista" v-if="party.Lista" >Lista: <a href="#" @click="toggleListaCard">{{ party.Lista }}</a></p>
                    <p class="lista" v-if="!party.Lista">Componenti: <a href="#">{{ party.Componenti}}</a></p>
                    <p class="alleanza">Alleanza: <a href="#">{{ party.Coalizione }}</a></p>
                    <a :href="party.Programma" class="link-programma">Programma Completo</a>
                    <p></p>
                </section>
            </div>
            <div class="" v-if="showListaCard">
            </div>
    </section>
</template>

<script>
import PartyDb from '../database/PartyDb.json'
import ListeDb from '../database/ListeDb.json'
export default{
    // Data
    data(){
        return{
            data: PartyDb,
            listdata: ListeDb,
            search: '',
            showListaCard: false,
            linkCard: ''
        }
    },


    methods: {
        // Mostrare la card delle liste
        toggleListaCard(){
            this.showListaCard = !this.showListaCard
        },

        // Link Wikipedia all'ideologia del partito
        Collocazionelink(Ideologia){
            if (Ideologia == 'Sinistra') {
                this.IdeologiaWiki = 'https://it.wikipedia.org/wiki/Sinistra_(politica)'
            } else if (Ideologia == 'Centro-Sinistra') {
                this.IdeologiaWiki = 'https://it.wikipedia.org/wiki/centro-sinistra'
            } else if (Ideologia == 'Centro') {
                this.IdeologiaWiki = 'https://it.wikipedia.org/wiki/centrismo'
            } else if (Ideologia == 'Centro-Destra') {
                this.IdeologiaWiki = 'https://it.wikipedia.org/wiki/centro-destra'
            } else if (Ideologia == 'Destra') {
                this.IdeologiaWiki = 'https://it.wikipedia.org/wiki/Destra_(politica)'
            } else {
                this.IdeologiaWiki = 'https://it.wikipedia.org/wiki/Trasversalismo'
            }
            return this.IdeologiaWiki
        },
    },

    computed: {
        // Searchbar codice
        SearchPartyField: function() {
            return this.data.filter((party) =>{
                return party.Nome.toLowerCase().match(this.search.toLowerCase()) ||
                        party.Collocazione.toLowerCase().match(this.search.toLowerCase());
            });
        },
    }
}
</script>

<style>
.overflow{
    overflow-y: fixed;
}
.header nav{
    display: flex;
    justify-content: space-between;
    padding: 1rem;
}
.header .title{
    font-size: 2rem;
    padding-left: 1rem;
    align-items: center;
    font-style: bold;
    margin: 0;
    padding: 0;
}
.seachbar{
    border: none;
    border-bottom: 1px solid #162841;
    margin-right: 1rem;
    width: 20rem;
}

.program-list {
    margin-left: 2rem;
    margin-right: 2rem;
    display: grid;
    grid-template-columns: repeat(5, 1fr);
    gap: 1rem;
    padding: 1rem;
    flex-wrap: wrap;
}
.card{
    box-sizing: border-box;
    margin: 0.8rem;
    border-radius: 15px;
    box-shadow: 0px 17px 77px -25px #4794ffa6;
}
.card img{
    padding: 0;
    width: 100%;
    object-fit: cover;
    border-radius: 15px 15px 0 0;
}
.card .card-content{
    padding-left: 1rem;
    padding-right: 1rem;
}
.link-programma{
    background-color: #162841;
    padding: .5em;
    border-radius: 5px;
    color: #fff;
}
.link-programma:hover{
    transition-duration: .6s;
    background-color: #0d1827;
}
.tipo {
    color: rgb(151, 151, 151);
    font-style: italic;
    padding-top: -1rem;
}

/* Colore Ideologia */

.sinistra{color: #780000;}
.centro-sinistra{color: #c1121f;}
.centro{color: #415a77;}
.centro-destra{color: #669bbc;}
.destra{color: #003049;}

/*  Media Query */

@media screen and (max-width: 1481px) {
    .program-list {
        grid-template-columns: repeat(4, 1fr);
        margin-left: 1rem;
        margin-right: 1rem;
    }
  }
  @media screen and (max-width: 1281px) {
    .program-list {
        grid-template-columns: repeat(3, 1fr);
        margin-left: 1rem;
        margin-right: 1rem;
    }
  }
  @media screen and (max-width: 850px) {
    .program-list {
        grid-template-columns: repeat(2, 1fr);
    }
    .header nav{
        flex-direction: column;
        justify-content: center;
    }
    .header nav .seachbar{
        margin-top: 2rem;
        width: 100%;
    }
  }
  @media screen and (max-width: 601px) {
    .program-list {
        grid-template-columns: repeat(1, 1fr);
        margin-left: 0rem;
        margin-right: 0rem;
    }
  }
</style>