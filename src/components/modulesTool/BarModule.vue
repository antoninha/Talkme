<template>
  <h2>{{ title }}</h2>
  <Bar :options="chartOptions" :data="chartData" />
</template>

<script setup>
import { Bar } from "vue-chartjs";
import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  BarElement,
  CategoryScale,
  LinearScale,
} from "chart.js";
import { computed } from "vue";

defineProps({
  title: String,
});

ChartJS.register(
  Title,
  Tooltip,
  Legend,
  BarElement,
  CategoryScale,
  LinearScale
);

const chartData = computed(() => ({
  labels: ["Janvier", "Février", "Mars", "Avril"],
  datasets: [
    {
      data: [40, 20, 12, 23],
      label: "Croissance",
      backgroundColor: ["#e5c380", "#e5c380", "#e5c380", "#CA8702"],
      borderRadius: "23",
    },
  ],
}));

const chartOptions = computed(() => ({ responsive: true }));
</script>

<style></style>
