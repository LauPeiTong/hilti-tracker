<template lang="pug">
  v-card.flexcard.pa-2.rounded-xl(outlined)
    v-card-text
      h3.fw-600.secondary--text Battery Status
      p.font-weight-regular.subtitle-2 Last checked: 06:48 PM, 24/1/2023

</template>

<script>
export default {
  name: 'BatteryStatus',
  props: {
    // eslint-disable-next-line vue/require-default-prop
    product: Object // pass product data as props
  },
  methods: {
    getColor (status) {
      if (status === 'Normal') {
        return this.$vuetify.theme.themes.light.green
      } else if (status === 'Checking') {
        return this.$vuetify.theme.themes.light.blue
      } else {
        return this.$vuetify.theme.themes.light.primary
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.border {
  border: solid 1px rgba(0, 0, 0, .2) !important;
}

.fw-600 {
  font-weight: 600 !important;
}

.flexcard {
  display: flex;
  flex-direction: column;
}
</style>
