<script>
  import { Bar } from 'vue-chartjs';

  export default {
    extends: Bar,
     props: {
      chartData: Array,
      months: Array,
    },
    watch: { 
      chartData: function(newVal) { // watch it
      this.data.datasets[0].data = newVal;
        this.renderChart(this.data, this.options);
      }
    },
    data () {
      return {
        data: {
          labels: this.months,
          datasets: [
            {
              label: 'Bookings number',
              data: this.chartData,
              fill: false,
              borderColor: '#2554FF',
              backgroundColor: '#2554FF',
              borderWidth: 1,
            }
          ]
        },
        options: {
          scales: {
            yAxes: [{
              ticks: {
                beginAtZero: true
              },
              gridBars: {
                display: false
              }
            }],
            xAxes: [ {
              gridBars: {
                display: true
              }
            }]
          },
          legend: {
            display: true
          },
          responsive: true,
          maintainAspectRatio: false
        },
      }
    },
    mounted () {
      this.renderChart(this.data, this.options);
    },
  }
</script>
<style>
#bar-chart {
  position: relative;
  width: 100%;
}
</style>
