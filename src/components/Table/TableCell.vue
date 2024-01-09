<template>
    <span class="tableCell" :class="{ tableCell__today: props.today }">
        <slot />
    </span>
</template>

<script setup>
import { defineProps } from 'vue';

const props = defineProps({
    today: {
        type: Boolean,
        default: false,
    },
});
</script>

<style lang="scss" scoped>
.tableCell {
    display: flex;
    background: var(--bg-grey);
    padding: 10px;
    align-items: center;
    justify-content: center;

    &__today {
        background: var(--light-blue);
    }
}
</style>
