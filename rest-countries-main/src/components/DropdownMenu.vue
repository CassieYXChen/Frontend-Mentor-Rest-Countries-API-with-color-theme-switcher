<script setup>
const REGIONS = ['All', 'Africa', 'America', 'Asia', 'Europe', 'Oceania', 'Pacific']
</script>

<template>
    <select :class="['dropdown dark:bg-dark-blue dark:text-white', 'btn']">
        <option v-for="region in REGIONS" :key="region" class="region-list">{{ region }}</option>
    </select>
</template>

<style>
.dropdown {
    margin: 0.75rem 1.25rem;
    width: 300px;
    height: 1rem;
    /* cursor: pointer; */
    border-radius: 0.25rem;
    padding: 0.625rem 1.25rem;
    box-shadow: 0 0 6px rgba(0, 0, 0, 0.1);
}

.btn {
    height: 2.75rem;
}

/* .region-list {
    appearance: none;
    cursor: pointer;
    height: 30px;
} */
</style>
