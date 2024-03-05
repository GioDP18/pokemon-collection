<template>
  <div class="whole">
    <div class="transparent">

      <!-- Head -->
      <div class="header">
        <h3 class="text-white">Top 3 Pokémon</h3>
        <q-btn-dropdown class="dd-buton" color="" label="Today">
          <q-list>
            <q-item clickable v-close-popup @click="onItemClick">
              <q-item-section>
                <q-item-label>Today</q-item-label>
              </q-item-section>
            </q-item>

            <q-item clickable v-close-popup @click="onItemClick">
              <q-item-section>
                <q-item-label>Yesterday</q-item-label>
              </q-item-section>
            </q-item>

            <q-item clickable v-close-popup @click="onItemClick">
              <q-item-section>
                <q-item-label>All</q-item-label>
              </q-item-section>
            </q-item>
          </q-list>
        </q-btn-dropdown>
      </div>

      <!-- Cards -->
      <div class="cards">
        <q-card class="my-card text-white">
          <q-card-section class="text-black">
            <div class="text-subtitle2">Top 1</div>
            <div class="text-h6">Mega Rayquaza</div>
          </q-card-section>

          <q-card-section class="text-black">
            aeppchwo
          </q-card-section>
        </q-card>
        <q-card class="my-card text-white">
          <q-card-section class="text-black">
            <div class="text-subtitle2">Top 2</div>
            <div class="text-h6">Mega Rayquaza</div>
          </q-card-section>

          <q-card-section class="text-black">
            aeppchwo
          </q-card-section>
        </q-card>
        <q-card class="my-card text-white">
          <q-card-section class="text-black">
            <div class="text-subtitle2">Top 3</div>
            <div class="text-h6">Mega Rayquaza</div>
          </q-card-section>

          <q-card-section class="text-black">
            aeppchwo
          </q-card-section>
        </q-card>
      </div>

      <!-- Table -->
      <div class="table-section">
        <table id="pokemonTable" class="table table-striped table-hover" width="100%;">
          <thead>
            <tr>
              <th>Pokemon</th>
              <th>Arrival</th>
              <th>Departure</th>
              <th>Late</th>
              <th>Number of Hours Worked</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="pokemon in pokemons" :key="pokemon">
              <th>{{ pokemon.name }}</th>
              <!-- <tr>
              <th>acas</th> -->
              <q-btn label="Click me" color="primary" @click="layout = true, getPokemonInfo(pokemon.name)" />


            </tr>
          </tbody>
        </table>
        <q-dialog v-model="layout">
          <q-layout view="Lhh lpR fff" container class="bg-white text-dark">

            <q-page-container>
              <q-page padding>
                <q-card-section style="width:33rem;">
                  <div style="display:flex; justify-content:center;">
                    <img :src="image" style="margin:auto; width:15rem; height:15rem">
                  </div>
                  <div class=" text-h6">Name: {{ name }}
                  </div>
                  <div class="text-subtitle2">Weight: {{ weight }}</div>

                  <p>Abilities:</p>
                  <ul>
                    <li v-for=" ability  in  abilities " :key="ability">
                      {{ ability.ability.name }}
                    </li>
                  </ul>
                </q-card-section>
              </q-page>
            </q-page-container>
          </q-layout>
        </q-dialog>
      </div>
    </div>
  </div>
</template>

<script setup>
import axios from "axios";
import { ref, onMounted } from "vue";
import $ from 'jquery';
import 'datatables.net-vue3';
import 'datatables.net-bs5';

const pokemons = ref([]);
const topThree = ref([]);
const layout = ref(false);

const image = ref('');
const name = ref('');
const abilities = ref([]);
const weight = ref('');

onMounted(async () => {
  initializeDataTables();
  getPokemons()
});

const initializeDataTables = () => {
  $(document).ready(function () {
    $('#pokemonTable').DataTable();
  });
}

const getTopThree = async () => {
  try {
    await axios.get('https://pokeapi.co/api/v2/pokemon?limit=3&offset=0')
      .then((response) => {
        topthree.value = response.data.results
      })
  }
  catch (error) {
    console.log(error);
  }
}

const getPokemons = async () => {
  try {
    await axios.get('https://pokeapi.co/api/v2/pokemon?limit=20&offset=0')
      .then((response) => {
        pokemons.value = response.data.results
      })
  }
  catch (error) {
    console.log(error);
  }
}

const getPokemonInfo = async (pName) => {
  try {
    await axios.get(`https://pokeapi.co/api/v2/pokemon/${pName}`)
      .then((response) => {
        console.log(response.data)
        image.value = response.data.sprites.front_default;
        name.value = response.data.name;
        abilities.value = response.data.abilities;
        weight.value = response.data.weight;
      })
  }
  catch (error) {
    console.log(error);
  }
}
</script>

<style lang="scss" scoped>
.whole {
  background-image: url('/images/pokemon.png');
  height: 13rem;
}

.transparent {
  height: 100vh;
  width: 75%;
  margin: auto;
  background-color: rgba(0, 0, 0, 0.5);
}

.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.header .dd-buton {
  background-color: #B64BFF;
  height: 2rem
}

.cards {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}

.my-card {
  width: 20rem;
  height: 15rem;
  border-radius: 8px;
}

.table-section {
  margin-top: 1rem;
}

.table-section .table {
  height: 400px;
  width: 100%;
  border-radius: 8px;
}
</style>
