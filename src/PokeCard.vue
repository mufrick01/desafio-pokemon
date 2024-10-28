<template>
  <article>
    <img :src="this.srcImg" :alt="`image del pokemon ${pokeName}`" :class="{'whoisthat':!correctName}">
    <h4 v-if="correctName" >{{ pokeName }}</h4>
    <div v-if="!correctName">
      <form @submit.prevent="clickHandler">
        <input v-model="inputText" type="text">
        <button type="submit">click</button>
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
        return 
      }

      this.correctName=true;
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
