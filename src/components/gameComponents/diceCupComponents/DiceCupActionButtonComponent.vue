<template>
  <q-btn type="button" style="margin-top: 5px" :id="this.id" class="q-ml-md" color="dark" @click="clickEvent"
         :disable="this.disabled">
    <span class="material-icons-outlined">
      <q-icon v-if="!this.isDiceButton" name="keyboard_double_arrow_left"/>
      <q-img v-else src="src/assets/images/flying_dices_small_white.png" width="40px"/>
    </span>
  </q-btn>
</template>

<script>
export default {
  props: {
    id: String,
    disabled: Boolean,
    isDiceButton: Boolean
  },
  methods: {
    clickEvent () {
      if (this.isDiceButton) {
        this.$emit('dice')
      } else {
        this.$emit('putAllIn')
      }
    }
  }
}
</script>

<style scoped>
.q-btn {
  min-height: 35px;
  height: 35px;
  width: 80px;
  font-size: 1.2em;
}

.q-btn .q-icon, .q-btn .q-spinner {
  vertical-align: baseline;
}

.q-ml-md {
  margin-left: 0;
}

</style>
