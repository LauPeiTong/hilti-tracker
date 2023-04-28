<template lang="pug">
v-row.tool-table.justify-center
  v-card.width-80.pa-4.rounded-xl
    v-card-title
      p Tool Status
      v-spacer
      v-text-field(
        v-model="search"
        append-icon="mdi-magnify"
        label="Search"
        single-line
        hide-details
      )
    v-data-table(
      :headers="headers"
      :items="desserts"
      :search="search"
    )
      template(v-slot:item.status="{ item }")
        v-chip(
          :color="getColor(item.status)"
          outlined
          pill
        )
          p.mb-0 {{ item.status }}
          v-icon.ml-2(v-if="item.status === 'Need Maintenance'" small) mdi-wrench
          v-icon.ml-2(v-if="item.status === 'Normal'" small) mdi-check-circle
          v-icon.ml-2(v-else small) mdi-clock-time-eight

      template(v-slot:item.action="{ item }")
        v-btn(
          icon
          :color="$vuetify.theme.themes.light.primary"
          :to="'/tooldetails'"
        )
          v-icon mdi-magnify
</template>

<script>
export default {
  name: 'ToolTable',
  data () {
    return {
      search: '',
      headers: [
        {
          text: 'Tools ID',
          align: 'start',
          sortable: false,
          value: 'id'
        },
        { text: 'Tools Name', value: 'name' },
        { text: 'Date & Time', value: 'dt' },
        {
          text: 'Status',
          align: 'center',
          value: 'status'
        },
        { text: 'Action', value: 'action' }
      ],
      desserts: [
        {
          id: 'T10-12118A',
          name: 'SID 4-A22 CORDLESS IMPACT DRIVER',
          dt: '06:48 PM, 24/1/2023',
          status: 'Normal',
          action: ''
        },
        {
          id: 'T10-12119A',
          name: 'TE 2-A22 CORDLESS ROTARY HAMMER',
          dt: '06:48 PM, 24/1/2023',
          status: 'Need Maintenance',
          action: ''
        },
        {
          id: 'T10-13418A',
          name: 'SID 4-A22 CORDLESS IMPACT DRIVER',
          dt: '06:48 PM, 24/1/2023',
          status: 'Checking',
          action: ''
        },
        {
          id: 'T10-12328A',
          name: 'BX 3 02 FASTENING TOOL',
          dt: '06:48 PM, 24/1/2023',
          status: 'Normal',
          action: ''
        },
        {
          id: 'T10-32342A',
          name: 'BX 3-BT (02) CORDLESS FASTENING TOOL',
          dt: '06:48 PM, 24/1/2023',
          status: 'Normal',
          action: ''
        },
        {
          id: 'T12-12111A',
          name: 'HDE 500-A22 CORDLESS',
          dt: '06:48 PM, 24/1/2023',
          status: 'Checking',
          action: ''
        },
        {
          id: 'T13-11238A',
          name: 'TE 2-A22 CORDLESS ROTARY HAMMER',
          dt: '06:48 PM, 24/1/2023',
          status: 'Need Maintenance',
          action: ''
        },
        {
          id: 'T20-75868A',
          name: 'HDE 500-A22 CORDLESS',
          dt: '06:48 PM, 24/1/2023',
          status: 'Normal',
          action: ''
        },
        {
          id: 'T22-12118B',
          name: 'TE 2-A22 CORDLESS ROTARY HAMMER',
          dt: '06:48 PM, 24/1/2023',
          status: 'Normal',
          action: ''
        },
        {
          id: 'T30-12118B',
          name: 'TE 2-A22 CORDLESS ROTARY HAMMER',
          dt: '06:48 PM, 24/1/2023',
          status: 'Checking',
          action: ''
        },
        {
          id: 'T10-12118A',
          name: 'SID 4-A22 CORDLESS IMPACT DRIVER',
          dt: '06:48 PM, 24/1/2023',
          status: 'Normal',
          action: ''
        }
      ]
    }
  },
  computed: {

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

<style scoped>
.width-80 {
  width: 90% !important;
}
</style>
