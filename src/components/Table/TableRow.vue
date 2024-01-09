<template>
    <div class="tableRow" @click="changeVisibleChart">
        <TableCell>{{ props.tableData.name }}</TableCell>
        <TableCell today>{{ numberFormat(props.tableData.today) }}</TableCell>
        <TableCell
            class="tableRow__statistic"
            :class="{
                positive: Boolean(
                    props.tableData.today > props.tableData.yesterday,
                ),
                negative: Boolean(
                    props.tableData.today < props.tableData.yesterday,
                ),
            }"
        >
            <span>{{ numberFormat(props.tableData.yesterday) }}</span>
            <span class="percent"
                >{{
                    percentCount(
                        props.tableData.today,
                        props.tableData.yesterday,
                    )
                }}%</span
            >
        </TableCell>
        <TableCell :class="props.tableData.weekDay.status">{{
            numberFormat(props.tableData.weekDay.value)
        }}</TableCell>
        <div v-if="isVisibleChart" class="tableRow__chart">
            <LineChart :chartData="props.tableData.chart" />
        </div>
    </div>
</template>

<script setup>
import { defineProps, ref, computed } from 'vue';
import TableCell from './TableCell.vue';
import LineChart from '../Charts/LineChart.vue';

const props = defineProps({
    tableData: {
        type: Object,
        required: true,
    },
});

const isVisibleChart = ref(false);

function changeVisibleChart() {
    isVisibleChart.value = !isVisibleChart.value;
}

function percentCount(cur, prev) {
    return Math.round((1 - prev / cur) * 100);
}

function numberFormat(value, locale = 'ru-RU', options = {}) {
    return new Intl.NumberFormat(locale, options).format(value);
}
</script>

<style lang="scss" scoped>
.tableRow {
    display: grid;
    grid-template-columns: 400px repeat(2, 150px) 170px;
    grid-template-areas:
        '. . . .'
        'chart chart chart chart';
    gap: 5px;
    cursor: pointer;

    @media (max-width: 1200px) {
        grid-template-columns: 400px repeat(2, 150px) 160px;
    }

    @media (max-width: 959px) {
        grid-template-columns: 200px repeat(2, 150px) 160px;
    }

    &__chart {
        display: grid;
        grid-area: chart;
        justify-items: center;
    }

    &__statistic {
        display: flex;
        justify-content: space-around;
        padding: 10px;
        width: 100%;
        .percent {
            color: var(--green);
        }
    }
    .positive {
        background: var(--light-green);
    }

    .negative {
        background: var(--light-red);
        .percent {
            color: var(--red);
        }
    }
}
</style>
