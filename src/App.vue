<template>
  <div id="app">
    <img alt="Vue logo" :src="imagen">
    <h1>pokemon</h1>
    <input type="text" v-model="nombre">
    <button @click="pokebusca">Buscar</button>
    <hr>
    <div v-for="(item, index) in imagenes" :key="index">
      <img :src="item" :alt="index">
    </div>
    <hr>
    <ul>
      <li v-for="(item, index) in habilidad" :key="index">{{item.ability.name}}</li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'App',
  data() {
    return {
      nombre: 'pikachu',
      habilidad: null,
      imagenes: null,
      imagen: require("./assets/logo.png"),
      url: 'https://www.digital55.com/wp-content/uploads/2019/09/%C2%BFQue%CC%81-debe-tener-un-profesional-especialista-en-Vue.png'
    }
  },
  methods: {
    pokebusca(){
      if (this.nombre) {
        axios.get(`https://pokeapi.co/api/v2/pokemon/${this.nombre}`)
        .then(response => {
          console.info(response.data.sprites);
          this.imagenes = response.data.sprites;
          this.habilidad = response.data.abilities;
        })
        .catch(error => {
          console.log(error)
          alert("El nombre no existe");  
        })
      }else {
        alert("No hay nombre para buscar");
      }
    }
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
</style>
