<template lang="pug">
.mx-auto
  ApexCharts(:options="options" :series="series")
</template>

<script>
export default {
  name: 'LineChart',
  data () {
    return {
      series: [{
        name: 'Desktops',
        data: [10, 41, 35, 51, 149, 62, 69, 21, 8]
      }],
      options: {
        chart: {
          height: 350,
          type: 'line',
          zoom: {
            enabled: false
          },
          background: '#FFFFFF' // set background color to white
        },
        dataLabels: {
          enabled: false,
          colors: ['#000000', 'transparent'] // set text color to black
        },
        stroke: {
          curve: 'straight'
        },
        title: {
          text: 'Temperature(°C)',
          align: 'left'
        },
        grid: {
          row: {
            colors: ['#f3f3f3', 'transparent'],
            opacity: 0.9
          }
        },
        xaxis: {
          categories: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep']
        },
        tooltip: {
          theme: 'light' // set tooltip theme to light
        }
      }
    }
  }
}
</script>
