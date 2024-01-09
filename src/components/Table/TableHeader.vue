<template>
    <div class="header">
        <TableCell
            v-for="header in props.headers"
            :today="header === 'Текущий день'"
            :key="header"
        >
            {{ header }}
        </TableCell>
    </div>
</template>

<script setup>
import { defineProps } from 'vue';
import TableCell from './TableCell.vue';

const props = defineProps({
    headers: {
        type: Array,
        required: true,
    },
});
</script>

<style lang="scss" scoped>
.header {
    display: grid;
    grid-template-columns: 400px repeat(2, 150px) 170px;
    gap: 5px;

    @media (max-width: 1200px) {
        grid-template-columns: 400px repeat(2, 150px) 160px;
    }

    @media (max-width: 959px) {
        grid-template-columns: 200px repeat(2, 150px) 160px;
    }
}
</style>
