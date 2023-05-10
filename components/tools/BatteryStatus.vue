<template lang="pug">
  v-card.flexcard.pa-2.rounded-xl(outlined)
    v-card-text
      h3.fw-600.secondary--text Battery Status
      p.font-weight-regular.subtitle-2 Last checked: 06:48 PM, 24/1/2023
      .d-flex.align-center.justify-center
        v-card.rounded-xl.battery-border.mb-2(height="100" width="210" outlined)
          .d-flex.fill-height
            v-card.rounded-xl.battery-remaining.mb-2.fill-height(outlined width="20%")
            v-card.rounded-xl.battery-remaining.mb-2.fill-height(outlined width="20%")
        v-card.battery-rounded.battery-border.mb-2(height="50" outlined)
      h3.fw-600.primary--text.mb-0.text-center 38%

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
.fw-600 {
  font-weight: 600 !important;
}

.flexcard {
  display: flex;
  flex-direction: column;
}

.battery-border {
  border: solid 8px #696667 !important;
}

.battery-remaining {
  background-color: #D2051E !important;
  border: solid 4px #ffffff !important;
}

.battery-rounded {
  border-radius: 0 24px 24px 0  !important;
}
</style>
