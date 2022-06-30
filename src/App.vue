<script setup lang="ts">
import {ref} from 'vue'
// import Add from './components/Add.vue'
import axios from 'axios'

// let pets = ref([])
// let newPet = ref({name: '', species: '', image: '', owner: '', notes: '', thoughts: ''})
let view = ref('main')

const addView = () => {
  view.value = 'add'
}
//
// const handleCreate = () => {
//   axios.post('https://forneverhome-backend.herokuapp.com/api/pets', newPet.value)
//   .then((response) =>{ pets.value = [...pets.value, response.data]
//   newPet.value = ref({name: '', species: '', image: '', owner: '', notes: '', thoughts: ''})
//   })
// }

</script>

<template>
  <header>
    <h1>For-Never Home</h1>
    <button @click="addView">Memorialize Your Pet</button>
  </header>
  <div class="add-form"> -->
    <!-- <Add :newPet="newPet" :handleCreate="handleCreate"/> -->
  </div>

</template>

<style>
@import './assets/base.css';

</style>
