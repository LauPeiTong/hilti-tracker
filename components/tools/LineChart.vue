<template lang="pug">
v-card.pa-4.rounded-xl(outlined)
  v-tabs.rounded-xl(vertical)
    v-tab(active)
      v-icon mdi-fire
    v-tab
      v-icon mdi-speedometer
    v-tab
      v-icon mdi-vibrate

    v-tab-item
      v-card.rounded-xl(outlined)
        v-card-text
          h3.fw-600.secondary--text Temperature
          p.font-weight-regular.subtitle-2 Today, 8/5/2023
          canvas(ref="chart" id="chart" height="100")

    v-tab-item
      v-card(flat)
        v-card-text
          p Sed aliquam ultrices mauris. Donec posuere vulputate arcu. Morbi ac felis. Etiam feugiat lorem non metus. Sed a libero.

    v-tab-item
      v-card(flat)
        v-card-text
          p Sed aliquam ultrices mauris. Donec posuere vulputate arcu. Morbi ac felis. Etiam feugiat lorem non metus. Sed a libero.

</template>

<script>
// import firebase from 'firebase/app'
// import 'firebase/database'
import firebase from 'firebase/compat/app'
import 'firebase/compat/database'
import Chart from 'chart.js/dist/Chart.js'

export default {
  data () {
    return {
      temperatureData: [],
      timestamps: [],
      rpmData: [],
      chart: null
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
    const temperatureRef = firebase.database().ref('test')

    // Listen for changes in the temperature and timestamp data
    temperatureRef.on('value', (snapshot) => {
      const data = snapshot.val()
      this.temperatureData = Object.values(data.temperature)
      this.timestamps = Object.values(data.timestamp)
      this.rpmData = Object.values(data.rpm)

      // Keep only the last 10 elements in the arrays
      if (this.temperatureData.length > 10) {
        this.temperatureData = this.temperatureData.slice(-10)
        this.rpmData = this.rpmData.slice(-10)
        this.timestamps = this.timestamps.slice(-10)
      }

      // Update the chart with the new data
      if (this.chart) {
        this.chart.data.datasets[0].data = this.temperatureData
        this.chart.data.datasets[1].data = this.rpmData
        this.chart.data.labels = this.timestamps
        this.chart.update()
      } else {
        this.createChart()
      }
      // // Check if a chart is already displayed
      // if (this.chart) {
      //   // Destroy the existing chart
      //   this.chart.destroy()
      // }
    })
  },
  methods: {
    createChart () {
      const ctx = document.getElementById('chart').getContext('2d')

      const gradient = ctx.createLinearGradient(0, 0, 0, 300)
      gradient.addColorStop(0, 'rgba(253, 126, 20, 1)')
      gradient.addColorStop(1, 'rgba(253, 126, 20, 0)')

      this.chart = new Chart(ctx, {
        type: 'line',
        data: {
          labels: this.timestamps,
          datasets: [
            {
              label: 'Temperature',
              data: this.temperatureData,
              borderColor: '#FD7E14',
              backgroundColor: gradient
            }
            // {
            //   label: 'Rpm',
            //   data: this.rpmData,
            //   borderColor: '#1890FF',
            //   backgroundColor: gradient
            // }
          ]
        },
        options: {
          scales: {
            yAxes: [{
              gridLines: {
                display: false
              },
              ticks: {
                beginAtZero: true
              }
            }],
            xAxes: [{
              gridLines: {
                display: false
              },
              ticks: {
                beginAtZero: true
              }
            }]
          }
        }
      })
    }
  }
}
</script>

<style lang="scss" scoped>
.fw-600 {
  font-weight: 600 !important;
}
</style>
