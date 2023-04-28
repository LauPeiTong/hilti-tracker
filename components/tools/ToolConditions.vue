##Temperature Current Vobration components
<template>
  <div class="d-flex justify-center" style="gap: 5px; padding: 100px;">
    <v-card class="mx-auto" max-width="180">
      <v-card-text>
        <div>Last checked value of</div>
        <p class="text-h5 text--primary">
          Current
        </p>
        <div class="text--primary">
          +55% since yesterday
        </div>
      </v-card-text>
    </v-card>

    <v-card class="mx-auto" max-width="180">
      <v-card-text>
        <div>Last checked value of</div>
        <p class="text-h5 text--primary">
          Temperature
        </p>
        <div class="text--primary">
          +23% since yesterday
        </div>
      </v-card-text>
    </v-card>

    <v-card class="mx-auto" max-width="180">
      <v-card-text>
        <div>Last checked value of</div>
        <p class="text-h5 text--primary">
          Vibration
        </p>
        <div class="text--primary">
          +36% since yesterday
        </div>
      </v-card-text>
    </v-card>
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
