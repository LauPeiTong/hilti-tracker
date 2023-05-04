##Temperature Current Vobration components
<template>
  <div class="d-grid">
    <v-row>
      <v-col :cols="4">
        <v-card class="mx-auto rounded-xl pa-4">
          <div>Last checked value of</div>
          <h2 class="">
            Current
          </h2>
          <div class="">
            +55% since yesterday
          </div>
        </v-card>
      </v-col>

      <v-col :cols="4">
        <v-card class="mx-auto rounded-xl pa-4">
          <div>Last checked value of</div>
          <h2>
            Temperature
          </h2>
          <div class="text-primary">
            +23% since yesterday
          </div>
        </v-card>
      </v-col>

      <v-col :cols="4">
        <v-card class="mx-auto rounded-xl pa-4">
          <div>Last checked value of</div>
          <h2>
            Vibration
          </h2>
          <div class="text-primary">
            +36% since yesterday
          </div>
        </v-card>
      </v-col>
    </v-row>
  </div>
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
