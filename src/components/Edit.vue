<script>
export default {
  props: ['handleUpdate', 'pet', 'editPet'],
  data(){
    return{

    }
  }
}
</script>

<template>
  <h2>Edit Page</h2>
  <details>
    <form @submit.prevent="handleUpdate(pet.id)">
      <input v-model="editPet.name" type="text">
      <input v-model="editPet.species" type="text">
      <input v-model="editPet.image" type="text">
      <input v-model="editPet.owner" type="text">
      <input v-model="editPet.notes" type="text">
      <input v-model="editPet.thoughts" type="text">
      <button type="submit">Submit</button>
    </form>
  </details>
</template>
