<template lang="pug">
  v-card.mx-auto.pa-2.rounded-xl(outlined)
    v-card-text
      h3.fw-600.secondary--text Status Analysis
      ApexCharts.d-flex.justify-space-around.pt-2(type="donut" :options="chartOptions" :series="series" width="250" height="250")

    v-card-title(class="text-center")
      b Prediction Accuracy
    v-card-subtitle(class="text-center")
      b 96.7%

    v-card-title(class="text-center")
      b Please repair before
    v-card-subtitle(class="text-center")
      b 31/1/2023

    v-card-title(class="text-center")
      b Repair Fee
    v-card-subtitle(class="text-center")
      b Free (within warranty period)

    v-card-actions
      v-space
</template>

<script>
export default {
  name: 'ToolRepair',
  data () {
    return {
      series: [34.4, 65.6],
      chartOptions: {
        chart: {
          type: 'donut'
        },
        legend: {
          show: false
        },
        labels: ['Normal', 'Need Maintenance'],
        colors: ['#F9F4F4', '#D2051E'],
        plotOptions: {
          pie: {
            expandOnClick: true,
            donut: {
              labels: {
                show: true,
                total: {
                  label: 'Accuracy',
                  showAlways: true,
                  show: true,
                  color: '#333333',
                  fontSize: '20px',
                  fontWeight: '600',
                  formatter: function (value) {
                    const t = 65.6
                    return t + '%'
                  }
                },
                value: {
                  color: '#333333',
                  fontSize: '28px',
                  fontWeight: '600'
                }
              }
            }
          }
        },
        responsive: [{
          breakpoint: 480,
          options: {
            chart: {
              width: 300
            },
            legend: {
              position: 'bottom'
            }
          }
        }],
        dataLabels: {
          enabled: false
        }
      }
    }
  }
}
</script>
