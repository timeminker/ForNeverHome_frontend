<script setup lang="ts">
import {ref, onMounted } from 'vue'
import Add from './components/Add.vue'
import axios from 'axios'


let pets = ref([])
let newPet: { name: string; species: string; image: string; owner: string; notes: string; thoughts: string; } = ref({name: '', species: '', image: '', owner: '', notes: '', thoughts: ''})
let view = ref('main')

const addView = () => {
  view.value = 'add'
}

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
    <button @click="addView">Memorialize Your Pet</button>
  </header>
  <div class="add-form"> -->
    <Add :newPet="newPet" :handleCreate="handleCreate"/>
  </div>

</template>

<style>
@import './assets/base.css';

</style>
