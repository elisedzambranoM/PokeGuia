<template>
  <div>
    <h1>Poke Guía</h1>
    <label for="">Nombre</label>
    <input type="text" v-model="pokemonName" />
    <button @click="searchPokemon">Buscar</button>
    <img
      v-if="currentPokemon.sprites"
      :src="currentPokemon.sprites.front_default"
      alt=""
    />
    <h2>Movimientos Pokemon</h2>
    <ul>
      <li v-for="move in moves" :key="move.name">
        {{ move.move.name }}
      </li>
    </ul>
    <h2>Habilidades Pokemon</h2>
    <ul>
      <li v-for="ability in abilities" :key="ability.name">
        {{ ability.ability.name }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      currentPokemon: {},
      pokemonName: "",
    };
  },
  created() {
    fetch(`https://pokeapi.co/api/v2/pokemon/pikachu`)
      .then((response) => response.json())
      .then((data) => (this.currentPokemon = data));
  },
  methods: {
    searchPokemon() {
      fetch(`https://pokeapi.co/api/v2/pokemon/${this.lower}`)
        .then((response) => response.json())
        .then((data) => (this.currentPokemon = data));
    },
  },
  computed: {
    moves() {
      return this.currentPokemon.moves;
    },
    abilities() {
      return this.currentPokemon.abilities;
    },
    lower() {
      return this.pokemonName.toLowerCase();
    },
  },
};
</script>


<style>
body {
  font-size: 30px;
}
input {
  font-size: 20px;
}
button {
  font-size: 20px;
}
ul {
  list-style-type: none;
}
</style>