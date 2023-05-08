<template lang="pug">
v-card
    v-tabs
      v-tab(v-for="(tab, index) in tabs" :key="index") {{ tab.name }}
      v-tab-item(v-for="(tab, index) in tabs" :key="index")
        canvas(ref="chart" :id="tab.id" height="100")
</template>

<script>
import firebase from 'firebase/compat/app'
import 'firebase/compat/database'
import Chart from 'chart.js/dist/Chart.js'

export default {
  data () {
    return {
      tabs: [
        { name: 'Temperature', id: 'temperature-chart', data: [] },
        { name: 'RPM', id: 'rpm-chart', data: [] }
      ]
    }
  },
  computed: {
    timestamps () {
      const data = this.tabs[0].data
      if (data.length > 0) {
        const start = new Date(data[0].timestamp)
        const end = new Date(data[data.length - 1].timestamp)
        const monthDiff = (end.getFullYear() - start.getFullYear()) * 12 + (end.getMonth() - start.getMonth()) + 1
        const timestamps = []
        for (let i = 0; i < monthDiff; i++) {
          const month = start.getMonth() + i
          const year = start.getFullYear() + Math.floor(month / 12)
          const label = `${year}-${month % 12 + 1}`
          timestamps.push(label)
        }
        return timestamps
      } else {
        return []
      }
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
    const temperatureRef = firebase.database().ref('test/temperature')
    const rpmRef = firebase.database().ref('test/rpm')

    // Listen for changes in the temperature data
    temperatureRef.on('value', (snapshot) => {
      const data = snapshot.val()
      this.tabs[0].data = Object.values(data)
      this.updateChart(0)
    })

    // Listen for changes in the RPM data
    rpmRef.on('value', (snapshot) => {
      const data = snapshot.val()
      this.tabs[1].data = Object.values(data)
      this.updateChart(1)
    })
  },
  methods: {
    createChart (tabIndex) {
      const tab = this.tabs[tabIndex]
      const ctx = document.getElementById(tab.id).getContext('2d')

      const gradient = ctx.createLinearGradient(0, 0, 0, 300)
      gradient.addColorStop(0, 'rgba(253, 126, 20, 1)')
      gradient.addColorStop(1, 'rgba(253, 126, 20, 0)')

      tab.chart = new Chart(ctx, {
        type: 'line',
        data: {
          labels: this.timestamps,
          datasets: [
            {
              label: tab.name,
              data: tab.data,
              borderColor: '#FD7E14',
              backgroundColor: gradient
            }
          ]
        },
        options: {
          scales: {
            xAxis: {
              title: {
                display: true,
                text: 'Month'
              }
            },
            yAxis: {
              title: {
                display: true,
                text: 'Value'
              }
            }
          }
        }
      })
    },

    updateChart (tabIndex) {
      const tab = this.tabs[tabIndex]

      if (tab.chart) {
        tab.chart.data.datasets[0].data = tab.data
        tab.chart.update()
      } else {
        this.createChart(tabIndex)
      }
    }
  }
}
