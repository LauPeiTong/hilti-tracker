<template lang="pug">
  v-card.white.pa-4.rounded-xl
    v-row.product
      v-col.product-image(:cols="12" md="4")
        v-img.border.rounded-xl(:src="product.image" alt="Product Image" max-height="200" contain)
      v-col.product-details(:cols="12" md="8")
        h2.mb-4 {{ product.name }}
        p.mb-1 Tool ID : {{ product.id }}
        p.mb-1 Warranty Date : {{ product.warranty }}
        p.mb-1 Last Checked Time : {{ product.checktime }}
        span.mb-1 Status :
          |
          v-chip.ml-2(
            :color="getColor(product.status)"
            outlined
            pill
          )
            p.mb-0 {{ product.status }}
            v-icon.ml-2(v-if="product.status === 'Need Maintenance'" small) mdi-wrench
            v-icon.ml-2(v-if="product.status === 'Normal'" small) mdi-check-circle
            v-icon.ml-2(v-if="product.status === 'Checking'" v-else small) mdi-clock-time-eight

</template>

<script>
export default {
  name: 'ToolDetails',
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

<style>
.border {
  border: solid 1px rgba(0, 0, 0, .2) !important;
}

</style>
