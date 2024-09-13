<template>
    <!-- Need to be two classes -->
    <div :class="['card bg-white', 'card dark:bg-darker-blue dark:text-white']" @click="showDetails">
        <img :src="country.flags.png" :alt="country.name.common" class="card-image" />
        <div class="text-container dark:bg-dark-blue">
            <h1 class="card-text">
                {{ country.name.common }}
            </h1>
            <p v-for="(detail, key) in countryDetails" :key="key" class="text-center text-sm font-semibold leading-8">
                {{ capitalize(key) }}:
                <span class="font-normal">{{ detail }}</span>
            </p>
        </div>
    </div>
</template>

<style>
.card {
    height: 350px;
    width: 300px;
    cursor: pointer;
    justify-content: center;
    align-items: center;
    margin: 1rem;
    border-radius: 5px;
    box-shadow: 0 0 6px rgba(0, 0, 0, 0.1);
}



.card:hover {
    opacity: 0.8;
}

.card-image {
    height: 170px;
    width: 300px;
    border-top-left-radius: 5px;
    border-top-right-radius: 5px;
}

.text-container {
    padding: 1.2rem;
    border-radius: 5px;
}

.card-text {
    margin-bottom: 1.25rem;
    text-align: center;
    font-size: 1.25rem;
}
</style>

<script setup>
import capitalize from 'lodash.capitalize'
import router from '../router'

const props = defineProps({
    country: {
        type: Object,
        required: true,
    },
})

const countryDetails = {
    population: props.country.population.toLocaleString(),
    region: props.country.region,
    capital: props.country.capital?.[0],
}

const showDetails = () => {
    const currentCountry = props.country.name.common.toLowerCase()
    router.push({ path: `/${currentCountry}` })
}
</script>
