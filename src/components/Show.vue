<script>
export default {
  props: ["pet"],
  data() {
    return {

    }
  }
}
</script>

<template>
  <div>
    <img v-bind:src="pet.image">
    <p>{{pet.name}}, a {{pet.species}} ID={{pet.id}}</p>
    <p>owned by {{pet.owner}}</p>
  </div>
</template>
