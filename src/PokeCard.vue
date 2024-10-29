<template>
  <article>
    <img :src="this.srcImg" :alt="`image del pokemon ${pokeName}`" :class="{'whoisthat':!correctName}">
    <h4 v-if="correctName" class="text-capitalize text-center p-0 m-0" >{{ pokeName }}</h4>
    <div v-if="!correctName">
      <form @submit.prevent="clickHandler">
        <input v-model="inputText" type="text" placeholder="Nombre del Pokémon" required>
        <button type="submit" class="btn btn-warning my-2 fw-bold">Descubrir</button>
      </form>
    </div>
  </article>
</template>

<script>
export default {
  name: 'PokeCard',
  data() {
    return {
      srcImg :`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${this.pokeNumber}.png`,
      correctName:false,
      inputText:'',
    };
  },
  props:{
      pokeName:String,
      pokeNumber:String,
  },
  methods:{
    clickHandler(){
      console.log(this.inputText);
      if(this.inputText.trim().toLocaleLowerCase() !== this.pokeName.toLocaleLowerCase()){

        this.inputText=''
        alert('El nombre no coincide con el Pokémon. Inténtalo nuevamente');
        return 
      }

      this.correctName=true;
      this.$emit('discovered-pokemon',true);
    }
  }
};
</script>

<style scoped>
/* Estilos aquí */

.whoisthat{
  filter: brightness(0);
}
article{
  display: flex;
  flex-direction: column;
  justify-content: center;
}
form{
  display: flex;
  flex-direction: column
}
</style>
