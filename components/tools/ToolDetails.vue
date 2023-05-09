<template lang="pug">
  v-card.pa-4.rounded-xl.flexcard(outlined)
    v-row.product
      v-col.product-image(:cols="12" md="4")
        v-img.border.rounded-xl(:src="product.image" alt="Product Image" max-height="200" contain)
      v-col.product-details(:cols="12" md="8")
        h2.mb-4.fw-600 {{ product.name }}
        p.mb-1.font-weight-medium Tool ID :
          |
          span.font-weight-regular  {{ product.id }}
        p.mb-1.font-weight-medium Warranty Date :
          |
          span.font-weight-regular  {{ product.warranty }}
        p.mb-1.font-weight-medium Last Checked Time :
          |
          span.font-weight-regular  {{ product.checktime }}
        span.mb-1.font-weight-medium Status :
          |
          v-chip.ml-2(
            :color="getColor(product.status)"
            outlined
            pill
          )
            p.mb-0 {{ getStatus() }}
            v-icon.ml-2(v-if="product.status === 'Need Maintenance'" small) mdi-wrench
            v-icon.ml-2(v-if="product.status === 'Normal'" small) mdi-check-circle
            v-icon.ml-2(v-if="product.status === 'Checking'" v-else small) mdi-clock-time-eight

</template>

<script>
import firebase from 'firebase/compat/app'
import 'firebase/compat/database'

export default {
  name: 'ToolDetails',
  props: {
    // eslint-disable-next-line vue/require-default-prop
    product: Object // pass product data as props
  },
  data () {
    return {
      // search: null
      statusData: []
    }
  },
  mounted () {
    // Initialize Firebase
    const firebaseConfig = {
      // Your Firebase config here
      apiKey: 'AIzaSyAW-sZ7INqOCLi2hNeYAr0lt0_wjURBhFY',
      authDomain: 'hilti-esp32.firebaseapp.com',
      databaseURL: 'https://hilti-esp32-default-rtdb.asia-southeast1.firebasedatabase.app',
      projectId: 'hilti-esp32',
      storageBucket: 'hilti-esp32.appspot.com',
      messagingSenderId: '502813794025',
      appId: '1:502813794025:web:28955fa05a3c585a0d1a78'
    }
    firebase.initializeApp(firebaseConfig)

    // Get reference to the 'test' node in Firebase
    const statusRef = firebase.database().ref('prediction')

    statusRef.on('value', (snapshot) => {
      const data = snapshot.val()
      this.statusData = Object.values(data.condition)

      // Keep only the last 10 elements in the arrays
      if (this.statusData.length > 1) {
        this.statusData = this.statusData.slice(-1)
      }
    })
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
    },
    getStatus () {
      return this.statusData[this.statusData.length - 1]
    }
  }
}
</script>

<style lang="scss" scoped>
.border {
  border: solid 1px rgba(0, 0, 0, .2) !important;
}

.fw-600 {
  font-weight: 600 !important;
}

.flexcard {
  display: flex;
  flex-direction: column;
}
</style>
