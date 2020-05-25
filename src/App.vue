<template>
  <div id="app">
    <h1>pokemon</h1>
    <input type="text" v-model="nombre">
    <button @click="pokebusca">Buscar</button>
    <hr>
    <hr>
    <div>
      <p>{{traerNombre}}</p>
      <div>
        <img :src="traerImg" alt="img">
      </div>
      <ul>
        <li v-for="(item, index) in habilidad" :key="index">{{item.ability.name}}</li>
      </ul>
      <ul>
        <li v-for="(item, index) in movimiento" :key="index">{{item.move.name}}</li>
      </ul>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'App',
  data() {
    return {
      datosCompletos: {
        name: '',
        sprites: {
          'front_default': ''
        }
      },
      validar: false,
      nombre: 'pikachu',
      habilidad: null,
      imagenes: null,
      movimiento: [],
      imagen: require("./assets/logo.png"),
      url: 'https://www.digital55.com/wp-content/uploads/2019/09/%C2%BFQue%CC%81-debe-tener-un-profesional-especialista-en-Vue.png'
    }
  },
  methods: {
    pokebusca(){
      if (this.nombre) {
        axios.get(`https://pokeapi.co/api/v2/pokemon/${this.nombre}`)
        .then(respuesta => {
          this.datosCompletos = respuesta.data;
          this.habilidad = respuesta.data.abilities;
          this.imagenes = respuesta.data.sprites.front_default;
          this.movimiento = respuesta.data.moves;
        })
        .catch(error => {
          console.log(error)
          alert("El nombre no existe");  
        })
      }else {
        alert("No hay nombre para buscar");
      }
    },
    async pikachu(){
      try {
        let respuesta = await axios.get('https://pokeapi.co/api/v2/pokemon/pikachu');
        console.info(respuesta.data);
        this.datosCompletos = respuesta.data;
        console.log(this.datosCompletos)
        this.habilidad = respuesta.data.abilities;
        this.imagenes = respuesta.data.sprites.front_default;
        this.movimiento = respuesta.data.moves;
        this.validar = !this.validar;
      } catch (error) {
        console.error(error);
      }
    },
    pikachu2(){
      axios.get('https://pokeapi.co/api/v2/pokemon/pikachu')
      .then(respuesta => {
        console.info(respuesta.data);
        this.datosCompletos = respuesta.data;
        console.log(this.datosCompletos)
        this.habilidad = respuesta.data.abilities;
        this.imagenes = respuesta.data.sprites.front_default;
        this.movimiento = respuesta.data.moves;
        this.validar = !this.validar;
      }).catch (error => console.error(error))
    }
  },
  mounted() {
    this.pikachu2();
  },
  computed: {
    traerNombre(){
      return this.datosCompletos.name
    },
    traerImg(){
      return this.datosCompletos.sprites.front_default
    },
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
