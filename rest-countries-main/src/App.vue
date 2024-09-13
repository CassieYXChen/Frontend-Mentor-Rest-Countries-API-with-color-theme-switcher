<script setup>
import { ref, onMounted, provide } from 'vue'
import Lookie from 'lookie'

import HeaderComponent from './components/Header.vue'

const countries = ref([])
const theme = ref(Lookie.get('theme') || 'dark')

onMounted(() => {
    fetch('https://restcountries.com/v3.1/all')
        .then((response) => response.json())
        .then((data) => {
            countries.value = data.sort((firstCountry, secondCountry) =>
                firstCountry.name.common.localeCompare(secondCountry.name.common)
            )
        })
})

provide('countries', countries)
provide('theme', theme)
</script>

<template>
    <div :class="theme">
        <HeaderComponent />
        <router-view />
    </div>
</template>

<style>
#app {
    height: 100%;
    width: 100%;
    margin: 0 auto;
    font-family: 'Nunito Sans', sans-serif;
}

.dark {
    height: 100vh;
    background: #202c37;
}
</style>
