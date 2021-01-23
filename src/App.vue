<template>
  <div id="app">
    
    <div class="column is-half is-offset-one-quarter">
     <h4 class="is-size-4"> Joelson Pires</h4>
     <hr> 
     <h4 class="is-size-4"> Lista de Pokemon</h4>
     <hr> 
     <input type="text"  class="input is-rounded" placeholder="Buscar Pokemon" v-model="busca">
     <button id="idBusca" class="button is-fullwidth is-success is-rounded" @click="buscar" >Buscar</button>
      <div v-for="(poke, index) in filteredPokemons" :key="poke.url">
        <Pokemon :name="poke.name" :url="poke.url" :num="index+1"></Pokemon>    
       </div>
    </div>   
  </div>
</template>
<script>

import axios from 'axios';
import Pokemon from './components/Pokemon';

export default {
  name: 'App',

  data(){
    return {
      pokemom :[],
      filteredPokemons:[],
      busca:''
    }
  },

  created:function() {
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(
      res => {
        this.pokemom = res.data.results;
        this.filteredPokemons = res.data.results;
      });  
  }, 
  components:{
    Pokemon
  },
  methods: {
    buscar:function (){
      this.filteredPokemons = this.pokemom;
        if(this.busca =='' || this.busca ==' '){
          this.filteredPokemons = this.pokemom;
        }else{
            this.filteredPokemons = this.pokemom.filter(pokemon => pokemon.name == this.busca);
        }
    }
  },
  computed:  {

    // resultadoBusca:function(){
    //   if(this.busca =='' || this.busca ==' '){
    //     return this.pokemom;
    //   }else{
    //     return this.pokemom.filter(pokemon => pokemon.name == this.busca)
    //   }
    // }
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#idBusca{
  margin-top: 2%;
}
</style>
