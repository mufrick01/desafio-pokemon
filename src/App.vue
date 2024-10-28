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
      this.HitApi();
    } catch (error) {
      throw Error(error);
    }
  },

  methods:{
    async HitApi(){
      const req = await fetch('https://pokeapi.co/api/v2/pokemon?limit=151');
      const resp = await req.json();

      
      this.pokeList = resp.results.map((pkm)=>{

        const number = pkm.url.split('/').at(-2)
        return{
          name:pkm.name,
          number,
        }
      })
    }
  }
}
</script>

<style>
#app {
  margin-top: 60px;
}
</style>
