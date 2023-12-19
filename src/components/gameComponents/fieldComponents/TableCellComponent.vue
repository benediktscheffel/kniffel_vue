<script>
import ActionButtonComponent from 'components/gameComponents/fieldComponents/ActionButtonComponent.vue'

export default {
  components: {
    ActionButtonComponent
  },
  props: {
    classAttribute: String,
    hasContent: Boolean,
    cellContent: String,
    hasIcon: Boolean,
    icon: String,
    hasSpan: Boolean,
    spanClassAttribute: String,
    spanContent: String,
    hasActionBtn: Boolean,
    actionBtnRow: Number,
    actionBtnActive: Boolean,
    actionBtnImgSrc: String,
    actionBtnActionText: String,
    isActive: Boolean,
    placeholder: String
  },
  methods: {
    writeTo() {
      this.$emit('writeTo')
    }
  }
}
</script>
<template>
  <q-td :class="this.classAttribute">
    <template v-if="this.hasContent">
      {{ this.cellContent }}
    </template>
    <template v-else-if="this.hasIcon">
      <q-icon :name="this.icon"/>
    </template>
    <template v-else-if="this.hasSpan">
      <template v-if="this.spanContent.length > 0">
        <span :class="this.spanClassAttribute">{{ this.spanContent }}</span>
      </template>
      <template v-else-if="placeholder !== undefined && placeholder.length > 0">
        <button :class="this.spanClassAttribute" class="placeholder" @click="writeTo" type="button">
          {{ this.placeholder }}
        </button>
      </template>

    </template>
    <template v-else>
      <action-button-component @writeTo="this.writeTo" :row="this.actionBtnRow" :active="this.actionBtnActive"
                               :img-src="this.actionBtnImgSrc" :action-text="this.actionBtnActionText">
      </action-button-component>
    </template>
  </q-td>
</template>
<style>
.secondColumn i {
  font-size: 25px;
}

.placeholder {
  color: grey;
  font-style: italic;
  width: inherit;
  background: inherit;
  height: inherit;
  border: unset;
}

button {
}
</style>
