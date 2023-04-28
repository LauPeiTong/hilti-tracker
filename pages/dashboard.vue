<template lang="pug">
.dashboard-page.fill-height.pa-0.ma-0
  v-row.pa-0.ma-0
</template>

<script>
import { mapGetters } from 'vuex'

export default {
  name: 'DashboardPage',
  components: {

  },
  layout: 'default',
  data () {
    return {
      // search: null
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

<style scoped>

</style>
