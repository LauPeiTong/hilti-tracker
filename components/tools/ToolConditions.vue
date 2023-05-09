<template lang="pug">
div.d-grid
  v-row
    v-col(:cols="4")
      v-card.mx-auto.rounded-xl.pa-4(outlined)
        div Last checked value of
        h2 RPM
        div +55% since yesterday
    v-col(:cols="4")
      v-card.mx-auto.rounded-xl.pa-4(outlined)
        div Last checked value of
        h2 Temperature
        div.text-primary +23% since yesterday
    v-col(:cols="4")
      v-card.mx-auto.rounded-xl.pa-4(outlined)
        div Last checked value of
        h2 Vibration
        div.text-primary +36% since yesterday

</template>

<script>
import { mapGetters } from 'vuex'

export default {
  name: 'ToolConditions',
  data () {
    return {
    }
  },
  computed: {
    ...mapGetters({
    })
  },
  methods: {
  }
}
</script>
