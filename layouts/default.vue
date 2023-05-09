<template lang="pug">
v-app
  v-main
    v-container.h-100.pa-0(fluid)
      v-row.ma-0.h-100.fill-width
        side-bar
        Nuxt
</template>

<script>
import SideBar from '../components/sidebar/SideBar'

export default {
  name: 'DefaultLayout',
  components: {
    SideBar
  },
  data () {
    return {
    }
  }
}
</script>
