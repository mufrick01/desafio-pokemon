<template>
  <div class="d-flex justify-content-center row">
    <img src="../src/assets/pkm-title.png" alt="" class="col-12 col-lg-6"/>
  </div>
  <h1 class="text-center">¿Quién es ese Pokémon?</h1>
  <p class="text-center"> Pokemons descubiertos: {{ discoverdPokemon }}/{{ totalPokemons }} </p>
  <div id="app" class="container mb-5">
    <div class="row">
      <PokeCard  v-for="(pokemon, index) in pokeList"   
      :key="`poke-${index}`"     
      :pokeName="pokemon.name" 
      :pokeNumber="pokemon.number" 
      class="col-12 col-lg-3" 
      @discovered-pokemon="onDiscoveredPokemon"
      />
    </div>
  </div>
  <footer>
    <hr/>
    <p class="text-capitalize text-center">Ningún derecho reservado</p>
  </footer>
</template>

<script>
import PokeCard from './components/PokeCard.vue';


export default {
  name: 'App',
  components: {
    PokeCard
  },
  data(){
    return{
      pokeList:[],
      discoverdPokemon:0,
      totalPokemons:20,
    }
  },
  created(){
    try {
      this.GetPokemonList();
    } catch (error) {
      throw Error(error);
    }
  },

  methods:{
    async GetPokemonList(){
      const req = await fetch('https://pokeapi.co/api/v2/pokemon?limit=151');
      const resp = await req.json();

      
      this.pokeList = resp.results.map((pkm)=>{

        const number = pkm.url.split('/').at(-2)
        return{
          name:pkm.name,
          number,
        }
      });




      for (let i = this.pokeList.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [this.pokeList[i], this.pokeList[j]] = [this.pokeList[j], this.pokeList[i]];
      }




      return this.pokeList = this.pokeList.slice(0, this.totalPokemons);
    },

    onDiscoveredPokemon(){
      this.discoverdPokemon++;
    }
  }
}
</script>

<style>
#app {
  margin-top: 60px;
}
</style>
