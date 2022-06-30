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
    <p>{{pet.name}}, a {{pet.species}} ID={{pet.id}}</p>
    <p>owned by {{pet.owner}}</p>
  </div>
</template>
