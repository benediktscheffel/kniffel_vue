<template>
  <q-header>
    <q-toolbar>
      <q-btn flat dense round to="/" class="q-mr-md">
        <q-avatar icon="home"/>
        Home
      </q-btn>

      <q-btn flat dense round to="/kniffel" id="actionGame">
        Game
      </q-btn>

      <q-space/>

      <q-btn flat dense round to="/about">
        About
      </q-btn>
    </q-toolbar>
  </q-header>
</template>

<script>
export default {
  name: 'NavBarComponent',
};
</script>

<style scoped>

</style>
