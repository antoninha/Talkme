<template>
  <h2>{{ title }}</h2>
  <Doughnut :options="chartOptions" :data="chartData" />
</template>

<script setup>
import { Doughnut } from "vue-chartjs";
import { Chart as ChartJS, ArcElement, Tooltip, Legend } from "chart.js";
import { computed } from "vue";

defineProps({
  title: String,
});

ChartJS.register(Tooltip, Legend, ArcElement);

const chartData = computed(() => ({
  labels: ["VueJs", "EmberJs", "ReactJs", "AngularJs"],
  datasets: [
    {
      data: [40, 20, 12, 23],
      label: "Croissance",
      backgroundColor: ["#e5c380", "#CA8702", "#e5c380", "#CA8702"],
    },
  ],
}));

const chartOptions = computed(() => ({ responsive: true }));
</script>

<style></style>
