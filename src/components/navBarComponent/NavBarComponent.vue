<template>
  <q-header>
    <q-toolbar class="bg-dark text-white">
      <q-btn flat dense to="/" class="q-mr-md" color="white">
        <q-avatar icon="home" text-color="white"/>
        Home
      </q-btn>
      <q-btn flat dense to="/kniffel" id="actionGame" color="white">
        Game
      </q-btn>
      <q-space/>
      <q-btn flat dense to="/about" color="white">
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
.q-toolbar.bg-dark {
  background-color: #343a40; /* Replace with your desired background color */
}

.q-toolbar.text-white {
  color: white; /* Replace with your desired text color */
}

.q-btn.color-white {
  color: white !important;
}

.q-btn.flat {
  background-color: transparent;
}

.q-btn.flat:hover {
  background-color: rgba(255, 255, 255, 0.1); /* Adjust the alpha value for the hover effect */
}

.q-btn.round {
  border-radius: 0; /* Adjust the border-radius as needed */
}

.q-avatar {
  margin-right: 5px;
}

</style>
