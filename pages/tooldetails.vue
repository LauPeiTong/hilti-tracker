<template lang="pug">
.tools-page.pa-0.ma-0.fill-width
  upper-title.ma-0(:title="'Tools Status'" :titleClass="'dark-background'")
  v-row.ma-0.pt-16.px-8.fill-width
    v-col(cols="9")
      tool-details.fill-height(:product="productData")
    v-col(cols="3")
      battery-status
    v-col(cols="9")
      //- tool-conditions
      line-chart
    v-col(cols="3")
      tool-repair.fill-height
</template>

<script>
import { mapGetters } from 'vuex'

import UpperTitle from '../components/UpperTitle.vue'

import ToolChartCopy from '../components/tools/ToolChartCopy.vue'
import ToolConditions from '../components/tools/ToolConditions.vue'
import ToolDetails from '../components/tools/ToolDetails.vue'
import ToolRepair from '~/components/tools/ToolRepair.vue'
import LineChart from '~/components/tools/LineChart.vue'
import LineChartCopy from '~/components/tools/LineChartCopy.vue'
import BatteryStatus from '~/components/tools/BatteryStatus.vue'

export default {
  name: 'ToolsPage',
  components: {
    UpperTitle,
    ToolChartCopy,
    ToolConditions,
    ToolDetails,
    ToolRepair,
    LineChart,
    LineChartCopy,
    BatteryStatus
  },
  layout: 'default',
  data () {
    return {
      // search: null
      productData: {
        name: 'SF 4-A22 CORDLESS DRILL DRIVER',
        id: 'T10-12118A',
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
