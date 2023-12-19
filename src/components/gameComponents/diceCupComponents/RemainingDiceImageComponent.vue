<template>
  <q-img src="src/assets/images/dicecup_small.png" :id="this.id" :style="{ opacity: this.opacity }"/>
</template>

<script>
export default {
  props: {
    id: String,
    opacity: Number
  }
}
</script>

<style scoped>

</style>
