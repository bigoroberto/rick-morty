<template>
  <div id="app">
    
    <div v-if="!loading" class="container text-center mt-5">
      <h1>Rick and Morty</h1>

      <!-- intercetto l'evento searchChar e invoco la funzione searching -->
      <search
      @searchCharacter="searching" />


      <div class="row">

        <!-- passo oggetto ciclato come comp card props -->
        <card 
         v-for="card in filteredCards"
        :key = "card.id"
        :card="card"
        />
      </div>

      <div class="text-center">
        <h6>Caratteri trovati: {{filteredCards.length}}</h6>
      </div>



    </div>


    <loader v-else/>


  </div>
</template>

<script>
import axios from 'axios'
 // . l'alias della cartella src è la @
import Card from './components/Card.vue'
import Loader from './components/Loader.vue'
import Search from './components/Search.vue'
export default {
  name: 'App',
  data(){
    return{
      axios,
      cards: Array,
      loading:true,
      textToSearch: ''
    }
  },
  created(){
    axios.get(' https://api.sampleapis.com/rickandmorty/characters')
    .then(res => {
      this.cards = res.data
      this.loading = false
      console.log(res.data)
    }) .catch (err => {
      console.log(err)
    })
  },
  components:{
    Card,
    Loader,
    Search
  },
  computed: {
    // . pulisce l'array cards e effettua la ricerca 
    filteredCards(){
      let cleanArr = this.cards.filter(item => item.name != undefined ) // ^ situa default solo se è buoto il txt search
      // se la stringa di ricerca è vuora restituisco l'array pulito
      if (this.textToSearch === '') {
        return cleanArr; 
      }
      // todo se la stringa di ricerca non è vuota filtro in base a essa
      return cleanArr.filter(item => item.name.toLowerCase().includes(this.textToSearch.toLowerCase()));
    }
  },
  methods: {
    // ! funzione richiamata da evento custom riceve come param il testo da cercare
    // mi serve per valorizzare il mio textToSeacrh x la ricerca
    searching(text){
      // . testo che cerchiamo dentro tutti i nomi
      // . di default è vuota e cambia quando la andiamo a valorizzare facendogli passare il nsotro evento custom
    
      this.textToSearch = text;
      /* console.log(text) */
    }
  }
}
</script>

<style lang="scss">
@import '@/assets/styles/general'
</style>