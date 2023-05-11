<template lang="pug">
  v-card.mx-auto.pa-2.rounded-xl(outlined)
    v-card-text
      h3.fw-600.secondary--text Status Analysis
      ApexCharts.d-flex.justify-space-around.pt-2(type="donut" :options="chartOptions" :series="series" width="250" height="250")

    v-card-text.pt-0(class="text-center")
      h3.fw-600.secondary--text Prediction Accuracy
      p.primary--text 65.6%

      h3.fw-600.secondary--text Please repair before
      p.secondary--text 31/8/2024

      h3.fw-600.secondary--text Repair Fee
      p.secondary--text Free (within warranty period)

      v-card.rounded-lg.mt-6.text-left(outlined)
        v-card-text
          p.mb-0 Last checked value of
          h2.secondary--text.fw-600.mb-5 Temperature
          h3.fw-600.primary--text +34%
            |
            span.font-weight-regular.grey--text  since yesterday

      v-card.rounded-lg.mt-6.text-left(outlined)
        v-card-text
          p.mb-0 Last checked value of
          h2.secondary--text.fw-600.mb-5 RPM
          h3.fw-600.primary--text +12%
            |
            span.font-weight-regular.grey--text  since yesterday

      v-card.rounded-lg.mt-6.text-left(outlined)
        v-card-text
          p.mb-0 Last checked value of
          h2.secondary--text.fw-600.mb-5 Vibration
          h3.fw-600.primary--text +27%
            |
            span.font-weight-regular.grey--text  since yesterday

      v-btn.primary.mt-6(depressed) Send to repair
        |
        v-icon.ml-2(small) mdi-wrench

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
                  color: '#D2051E',
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

<style scoped>
.fw-600 {
  font-weight: 600 !important;
}
</style>
