<template>
  <div>
    <form class="d-flex mb-5 mt-5">
      <div class="flex-grow-1 ">
        <input
        @keyup.enter="startSearch"
        v-model.trim="stringToSearch" 
        placeholder="Search..."
        class="form-control"
        type="text">
      </div>
      <!-- uso prevent x non refreshare la pagina -->
      <div>
        <button 
        @click.prevent="startSearch"
        class="btn btn-primary ms-3">
        Search</button>
      </div>
      <div>
        <button
        @click.prevent="resetSearch"
        class="btn btn-warning ms-3">
        Reset</button>
      </div>
      
    </form>

  </div>
</template>

<script>
export default {
name: 'Search',
data(){
  return{
    stringToSearch: ''
  }
},
methods:{
  // metodo richiamato da click e key up che generano un evento custom
  startSearch(){
    this.$emit("searchCharacter", this.stringToSearch) // ^ io scateno l'evento search char e gli passo come param la stringa da cercare
  },
  // chiamato da reset pulisce il testo da ricercare e richiama la func di recerca
  resetSearch(){
    this.stringToSearch = "" // ^ qua pulisco la stringa e BASTA
    this.startSearch(); // . qua richiamo l'evento che scatena la ricerca e quindi mi passa una stringa vuota
  }
},
}
</script>

<style>
</style>