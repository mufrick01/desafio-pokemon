<template>
  <h1 class="text-center">¿Quién es ese Pokémon?</h1>
  <div id="app" class="container">
    <div class="row">
      <PokeCard  v-for="(pokemon, index) in pokeList"   :key="`poke-${index}`"     :pokeName="pokemon.name" :pokeNumber="pokemon.number" class="col-6 col-lg-3" />
    </div>
  </div>
</template>

<script>
import PokeCard from './PokeCard.vue';


export default {
  name: 'App',
  components: {
    PokeCard
  },
  data(){
    return{
      pokeList:[]
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




      return this.pokeList = this.pokeList.slice(0, 16);
    }
  }
}
</script>

<style>
#app {
  margin-top: 60px;
}
</style>
