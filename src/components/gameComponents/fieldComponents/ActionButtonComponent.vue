<script>
export default {
  props: {
    row: Number,
    active: Boolean,
    imgSrc: String,
    actionText: String
  },
  methods: {
    writeTo () {
      this.$emit('writeTo')
    }
  }
}
</script>
<template>
  <button type="button"
         class="btnAction"
         @click="writeTo"
         :disabled="this.active">
    <template v-if="this.row < 7">
      <img :src="this.imgSrc" />
    </template>
    <template v-else>
      {{this.actionText}}
    </template>
  </button>
</template>
<style>
  button.btnAction {
    height: 100%;
    width: 100%;
    border: none;
  }

  .btnAction img {
    height: 100%;
    width: auto;
  }
</style>
