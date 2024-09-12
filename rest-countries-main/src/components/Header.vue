<script setup>
import router from '../router'
import ModeSwitcher from './ModeSwitcher.vue'
</script>

<template>
    <div class="header dark:bg-dark-blue">
        <h1 class="title dark:text-white">Where in the world?</h1>
        <div>
            <ModeSwitcher />
        </div>
    </div>
</template>

<style>
.header {
    position: relative;
    height: 100px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    box-shadow: 0 0 8px rgba(0, 0, 0, 0.1);
}

.title {
    font-weight: 900;
    font-size: 18px;
    padding-left: 60px;
}
</style>
