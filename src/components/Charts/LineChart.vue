<template>
    <Line :data="props.chartData" :options="options" />
</template>

<script setup>
import { ref, defineProps } from 'vue';
import {
    Chart as ChartJS,
    CategoryScale,
    LinearScale,
    PointElement,
    LineElement,
    Title,
    Tooltip,
    Legend,
} from 'chart.js';
import { Line } from 'vue-chartjs';

ChartJS.register(
    CategoryScale,
    LinearScale,
    PointElement,
    LineElement,
    Title,
    Tooltip,
    Legend,
);

const props = defineProps({
    chartData: {
        type: Object,
        required: true,
    },
});

const options = ref({
    responsive: true,
    maintainAspectRatio: false,
});
</script>
