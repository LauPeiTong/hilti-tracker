<template lang="pug">
v-row.fincare-search-bar.px-6
  v-text-field.pt-0.mt-0.rounded-lg(
    v-model="modelValue"
    label="Search"
    single-line
    hide-details
    solo
  )
    template(v-slot:prepend-inner)
      client-only
        eva-icon(name="search-outline" height="20" :fill="$vuetify.theme.themes.light.secondary")

</template>

<script>
export default {
  name: 'FSearchBar',
  props: {
    value: {
      type: String,
      default: null
    }
  },
  computed: {
    modelValue: {
      get () {
        return this.value
      },
      set (newValue) {
        this.$emit('change', newValue)
      }
    }
  }
}
</script>

<style scoped>
:deep(.v-text-field .v-input__slot){
  min-height: 40px;
}

:deep(.font-18px) {
  font-size: 18px;
}

.fincare-search-bar {
  position: absolute;
  top: 70px;
  width: 100%;
  z-index: 100;
}
</style>
