<script setup lang="ts">
import {ref, onMounted } from 'vue'
import Add from './components/Add.vue'
import Show from './components/Show.vue'
import Edit from './components/Edit.vue'
import axios from 'axios'


let pets = ref([])
let newPet = ref({name: '', species: '', image: '', owner: '', notes: '', thoughts: ''})
let editPet = ref({name: '', species: '', image: '', owner: '', notes: '', thoughts: ''})
let view = ref('main')

let filterResults = ref([])
// let foundDogs = ref([])
// let foundCats = ref([])
// let foundReptiles = ref([])

// view functions
const addView = () => {
  view.value = 'add'
}
const mainView = () => {
  view.value = 'main'
}

// filtering function by animal
const filter = (animal) => {
  filterResults.value = pets.value.filter(pet => pet.species === animal)
  view.value = 'filter'
}

// CRUD API functions
onMounted(() => {
  axios.get('https://forneverhome-backend.herokuapp.com/api/pets')
  .then((response) =>{ pets.value = response.data
    console.log(pets)
  })
})

const handleCreate = () => {
  axios.post('https://forneverhome-backend.herokuapp.com/api/pets', newPet.value)
  .then((response) =>{ pets.value = [...pets.value, response.data]
  newPet.value = ref({name: '', species: '', image: '', owner: '', notes: '', thoughts: ''})
  })
}

const handleUpdate = (petID) => {
  axios.put('https://forneverhome-backend.herokuapp.com/api/pets/' + petID, editPet.value)
  .then((response)=> {
    editPet.value = ref({name: '', species: '', image: '', owner: '', notes: '', thoughts: ''})
    pets.value = pets.value.map((pet) => {
      return pet.id !== response.data.id ? pet : response.data
    })
  })
}

const handleDelete = (petID: number) => {
  axios.delete('https://forneverhome-backend.herokuapp.com/api/pets/' + petID)
  .then((response) => {
    pets.value = pets.value.filter(pet => pet.id !== petID)
  })
}

</script>

<template>
  <header>
    <h1>For-Never Home</h1>
  </header>
  <main v-if="view == 'main'">
    <button @click="addView">Memorialize Your Pet</button>
    <button @click="filter('Dog')">Show Dogs</button>
    <button @click="filter('Cat')">Show Cats</button>
    <button @click="filter('Reptile')">Show Reptiles</button>
    <div class="container">
      <div v-for="pet in pets" :key="pet.id" class="card">
        <Show :pet="pet"/>
        <Edit :pet="pet" :editPet="editPet" :handleUpdate="handleUpdate"/>
        <button @click="handleDelete(pet.id)">Delete</button>
      </div>
    </div>

  </main>
  <div class="add-form" v-if="view == 'add'">
    <button @click="mainView">Return to Hall Of Rememeberance</button>
    <Add :newPet="newPet" :handleCreate="handleCreate"/>
  </div>
  <section v-if="view == 'filter'">
    <div v-for="animal in filterResults" :key="animal.id">
      <p>{{animal.name}}, a go od {{animal.species}}</p>
      <p>owned by {{animal.owner}}</p>
    </div>
    <button @click="mainView">Return to Hall Of Rememeberance</button>
  </section>
</template>

<style>
@import './assets/base.css';

</style>
