<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <h1>pokemon</h1>
    <input type="text" v-model="nombre">
    <button @click="pokebusca">Buscar</button>
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
      habilidad: null
    }
  },
  methods: {
    pokebusca(){
      if (this.nombre) {
        axios.get(`https://pokeapi.co/api/v2/pokemon/${this.nombre}`)
        .then(response => {
          console.info(response.data.abilities[0]);
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
