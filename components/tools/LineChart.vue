<template>
  <div>
    <canvas ref="chart"></canvas>
  </div>
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

      // Update the chart with the new data
      if (this.chart) {
        this.chart.data.datasets[0].data = this.temperatureData
        this.chart.data.labels = this.timestamps
        this.chart.update()
      } else {
        this.createChart()
      }
    })
  },
  methods: {
    createChart () {
      this.chart = new Chart(this.$refs.chart.getContext('2d'), {
        type: 'line',
        data: {
          labels: this.timestamps,
          datasets: [
            {
              label: 'Temperature',
              data: this.temperatureData,
              borderColor: 'rgba(75, 192, 192, 1)',
              backgroundColor: 'rgba(75, 192, 192, 0.2)'
            }
          ]
        },
        options: {
          scales: {
            x: {
              type: 'time',
              time: {
                unit: 'minute'
              }
            },
            y: {
              ticks: {
                beginAtZero: true
              }
            }
          }
        }
      })
    }
  }
}
</script>
