<template>
  <div class="pie-chart">
    <pie-chart :data="chartData" :options="chartOptions" />
  </div>
</template>

<script>
import { ref, onMounted, onBeforeUnmount } from 'vue';
import { Pie } from 'vue-chartjs';
import axios from 'axios';

export default {
  name: 'PieChart',
  extends: Pie,
  setup() {
    const chartData = ref(null);
    const chartOptions = ref({
      responsive: true,
      maintainAspectRatio: false,
    });

    const fetchData = async () => {
      try {
        const response = await axios.get('https://example-api.com/pie-chart-data');
        chartData.value = response.data; // Assuming the API response provides appropriate chart data
      } catch (error) {
        console.error('Error fetching data:', error);
      }
    };

    onMounted(() => {
      fetchData();
    });

    onBeforeUnmount(() => {
      // Clean up code here
    });

    return {
      chartData,
      chartOptions,
    };
  },
};
</script>

<style scoped>
.pie-chart {
  width: 100%;
  max-width: 400px;
  margin: 0 auto;
}
</style>
