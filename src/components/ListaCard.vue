<template>
    <section class="coalition">
        <div class="bg-black"></div>
        <div class="x" v-for="list in listdata" :key="list.id">
        <h1>{{list.Nome}}</h1>
        </div>
        <div class="coalition-box" v-for="list in listdata" :key="list.id">
        <div class="match" v-if="matchListaCard = list.Nome">
            <header class="coalition-header" >
                <a href="#" class="close-popup" @click="closeListaCard"> 
                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="#fff" stroke-width="3" stroke-linecap="round" stroke-linejoin="round" class="feather feather-x"><line x1="18" y1="6" x2="6" y2="18"></line><line x1="6" y1="6" x2="18" y2="18"></line></svg>
                </a> 
                <img src="../assets/Img/IaC-banner.jpg" alt="">
                <h2>{{ list.Nome }}</h2>
            </header>
            <p class="tipo">Lista</p>
            <div class="collocazione"> <p>Collocazione: {{ list.Collocazione }}</p> </div>
            <div class="party-list-box">
                <h3>Partiti:</h3>
                <ul v-for="listmember in list.Componenti" :key="listmember.partyId">
                    <li>{{ listmember.Sito }}</li>
                </ul>
                <a href="#" class="link-programma">Programma Completo</a>
                <br>
                <p>{{ listdata }}</p>
            </div>
        </div>
        </div>
    </section>

</template>

<script>
import ListeDb from '../database/ListeDb.json'

export default {
    props: [this.showListData],
        data(){
        return{
            listdata: ListeDb,
        }
    },

    methods: {
        closeListaCard(){
            this.$emit('close')
            console.log(this.matchListaCard)
        },
    }
}
</script>

<style scoped>
.coalition {
    display: flex;
}
.coalition .bg-black{
    overflow-y:scroll;
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    background-color: rgba(0, 0, 0, 0.5);
}
.coalition .coalition-box{
    background-color: #fff;
    position: fixed;
    overflow-y:scroll;
    top: 10px;
    bottom: 10px;
    left: 30%;
    right: 30%;
    margin: 2rem;
    box-shadow: 1px -1px 70px -10px rgba(71,148,255,.3);
    border-radius: 15px ;
}
.coalition .coalition-box .coalition-header{
    position: relative;
}
.coalition .coalition-box .coalition-header .close-popup{
    position: absolute;
    border-radius: 100px;
    width: 20px;
    height: 20px;
    right: 10px;
    top: 10px;
    background-color: red;
}
.coalition .coalition-box .coalition-header .close-popup svg {
    position: absolute;
    top: 10%;
    left: 10%;
}

.coalition .coalition-box .coalition-header img{
    border-radius: 15px 15px 0 0;
    width: 100%;
}
.coalition .coalition-box h2, h3, li, .link-programma, p {
    margin: 1rem;
    margin-top: 0rem;
    margin-bottom: 0;
}
.tipo {
    color: rgb(151, 151, 151);
    font-style: italic;
    padding-top: 1rem;
    padding-bottom: 0.5rem;
}
.link-programma{
    margin-top: 0.5rem;
    background-color: #162841;
    padding: .5em;
    border-radius: 5px;
    color: #fff;

}
.coalition .coalition-box li {
    padding: .4rem;
}

/*  Media Query */

@media screen and (max-width: 1481px) {
    /* .coalition .coalition-box{
    left: 20%;
    right: 20%;
    margin: 2rem;
} */
  }
@media screen and (max-width: 1281px) {
    .coalition .coalition-box{
        left: 25%;
        right: 25%;
        margin: 2rem;
    }
}
@media screen and (max-width: 850px) {
    .coalition .coalition-box{
        left: 10%;
        right: 10%;
        margin: 2rem;
    }
}
@media screen and (max-width: 601px) {
    .coalition .coalition-box{
        left: 1%;
        right: 1%;
        margin: 1rem;

    }
}
</style>