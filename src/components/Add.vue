<template>
  <form @submit.prevent="handleCreate">
    <label htmlFor="name">Name</label>
    <input v-model="newPet.name" type="text"><br/>
    <label htmlFor="species">Species</label>
    <input v-model="newPet.species" type="text"><br/>
    <label htmlFor="image">Image</label>
    <input v-model="newPet.image" type="text"><br/>
    <label htmlFor="owner">Owner</label>
    <input v-model="newPet.owner" type="text"><br/>
    <label htmlFor="notes">Description</label>
    <input v-model="newPet.notes" type="text"><br/>
    <label htmlFor="thoughts">Thoughts and Prayers</label>
    <input v-model="newPet.thoughts" type="text"><br/>
    <button type="submit">Submit</button>
  </form>
</template>

<script>
export default {
  props: ['handleCreate', 'newPet'],
  data() {
    return {

    }
  }
}
</script>

<style>
</style>
