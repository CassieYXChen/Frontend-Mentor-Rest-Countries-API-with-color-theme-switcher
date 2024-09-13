<template>
    <div class="nav-bar bg-dark-white dark:bg-darker-blue">
        <SearchBox v-model="searchedCountry" @clearSearch="clearSearch" />
        <DropdownMenu @change="regionUpdate" />
    </div>
    <div class="cards bg-dark-white dark:bg-darker-blue">
        <CountryCard v-for="country in filteredCountryList" :key="country.name.common" :country="country" />
    </div>
</template>

<style>
.nav-bar {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-wrap: wrap;
}

.cards {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-wrap: wrap;
    gap: 20px;
}

@media (min-width: 768px) {
    .nav-bar {
        justify-content: space-between;
        padding: 3rem;
    }
}
</style>

<script setup>
import { ref } from 'vue'
import { computed } from 'vue'

import SearchBox from './SearchBox.vue'
import CountryCard from './CountryCard.vue'
import DropdownMenu from './DropdownMenu.vue'

const props = defineProps({
    countries: {
        type: Array,
        required: true,
    },
})

const selectedRegion = ref('All')
const searchedCountry = ref('')

const regionUpdate = (e) => (selectedRegion.value = e.target.value)
const clearSearch = () => (searchedCountry.value = '')

const regionalCountryList = computed(() => {
    return props.countries.filter((country) =>
        selectedRegion.value === 'All' ? props.countries : country.region === selectedRegion.value
    )
})

const searchedCountryList = computed(() => {
    return regionalCountryList.value.filter((country) =>
        country.name.common.toLowerCase().includes(searchedCountry.value.toLowerCase())
    )
})

const filteredCountryList = computed(() => {
    if (searchedCountry.value) {
        return searchedCountryList.value
    } else {
        return regionalCountryList.value
    }
})
</script>
