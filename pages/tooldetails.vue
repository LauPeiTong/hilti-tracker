<template lang="pug">
.tools-page.pa-0.ma-0.fill-width
  upper-title.ma-0(:title="'Tools Status'" :titleClass="'dark-background'")
  v-row.ma-0.pt-8.fill-width
    v-col(cols="12")
      tool-details(:product="productData")
    v-col(cols="8")
      tool-conditions
    v-col(cols="4")
      tool-repair
</template>

<script>
import { mapGetters } from 'vuex'

import UpperTitle from '../components/UpperTitle.vue'

import ToolChartCopy from '../components/tools/ToolChartCopy.vue'
import ToolConditions from '../components/tools/ToolConditions.vue'
import ToolDetails from '../components/tools/ToolDetails.vue'
import ToolRepair from '~/components/tools/ToolRepair.vue'

export default {
  name: 'ToolsPage',
  components: {
    UpperTitle,
    ToolChartCopy,
    ToolConditions,
    ToolDetails,
    ToolRepair
  },
  layout: 'default',
  data () {
    return {
      // search: null
      productData: {
        name: 'SF 4-A22 CORDLESS DRILL DRIVER',
        id: '1234',
        warranty: '2023-06-25',
        status: 'Normal',
        checktime: '6:00 PM, 4/1/2023',
        image: 'https://shorturl.at/MPRV6'
      }
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
:deep(.scroll) {
  overflow-x: hidden;
  overflow-y: auto;
  width: 100% !important;
}

.fill-width {
  width: 100% !important;
}
</style>
