<script>
import { ref, onMounted } from 'vue';

export default {
  setup() {
    const pokemons = ref({});
    onMounted(async () => {
      const response = await fetch('https://pokeapi.co/api/v2/pokemon?limit=905&offset=0');
      const data = await response.json();
      const results = await Promise.all(data.results.map(async pokemon => {
        const res = await fetch(pokemon.url);
        return await res.json();
      }));
      pokemons.value = results
    });
    return { pokemons };
  }
};
</script>

<template>
  <body>
    <div class="poke-container" id="poke-container">
      
      
      
      <ul>
        <li class="pokemon" v-for="pokemon in pokemons" :key="pokemon.name">
          {{ pokemon.name }}
          <div class="img-container"> 
            <img :src="pokemon.sprites?.front_default" />
          </div>
        </li>
      </ul>
    </div>
  </body>
    </template>
    <style lang="scss" scoped>
    body {
  background: #efefbb;
  background: linear-gradient(to right, #d4d3dd, #efefbb);
  font-family: 'Lato', sans-serif;
  display: grid;
  
  margin: 0 auto;
      #poke-container {
        margin: 18% 0 0 0;
        width: 100%;
        display: grid;
          ul {
            display: grid;
             width: 100%;
             grid-template-columns: repeat(4, 1fr);
              li {
                display: grid;
                justify-content: center;
                background-color: #eee;
                box-shadow: 0 3px 15px rgba(100, 100, 100, 0.5);
                margin: 5%;
                list-style: none;
                text-transform: uppercase;
                text-align: center;
                padding: 1% 0 1% 0;
                .img-container {
                  display: grid;
                  
                }
              }
          }
        
      }
}

// .poke-container {
//   display: grid;
//   flex-wrap: wrap;
//   align-items: space-between;
//   justify-content: center;
//   margin: 0 auto;
//   max-width: 1200px;
// }
// .pokemon {
//   background-color: #eee;
//   border-radius: 10px;
//   box-shadow: 0 3px 15px rgba(100, 100, 100, 0.5);
//   margin: 10px;
//   padding: 20px;
//   text-align: center;
// }
// .pokemon .img-container {
//   background-color: rgba(255, 255, 255, 0.6);
//   border-radius: 50%;
//   width: 120px;
//   height: 120px;
//   text-align: center;
//   ;
// }
//  .img-container img {
//   align-items: center;

// }
// .pokemon .img-container img {
//   max-width: 90%;
//   margin-top: 20px;
// } 
</style>
