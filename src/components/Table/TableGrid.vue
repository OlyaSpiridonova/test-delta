<template>
    <div class="table">
        <TableHeader :headers="tableHeaders" />
        <BaseLoader v-if="isLoading" />
        <TableRow
            v-else
            v-for="data in tableData"
            :table-data="data"
            :key="data.name"
        />
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import TableHeader from './TableHeader.vue';
import TableRow from './TableRow.vue';
import BaseLoader from '../UI/BaseLoader.vue';

const isLoading = ref(true);

const tableHeaders = ref([
    'Показатель',
    'Текущий день',
    'Вчера',
    'Этот день недели',
]);

const tableData = ref(null);

onMounted(async () => {
    try {
        const res = await fetch('https://delta-server-iota.vercel.app/data');
        tableData.value = await res.json();
    } catch (error) {
        throw error;
    } finally {
        isLoading.value = false;
    }
});
</script>

<style lang="scss" scoped>
.table {
    display: grid;
    justify-items: center;
    grid-auto-flow: row;
    gap: 5px;
    padding: 10px;
    border: 3px solid #dddddd;
    color: grey;
    font-weight: 500;
    font-size: 14px;
    @media (max-width: 779px) {
        overflow: scroll;
    }
}
</style>
