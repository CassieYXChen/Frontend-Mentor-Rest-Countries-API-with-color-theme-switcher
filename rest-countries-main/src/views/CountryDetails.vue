<template>
    <div class="dark:bg-darker-blue dark:text-white">
        <button :class="['back-btn bg-white dark:bg-dark-blue dark:text-white', 'btn-container']" @click="returnHome">
            <Icon name="arrow" :size="18" class="arrow" />
            <span class="text">Back</span>
        </button>
    </div>
    <div class="details dark:bg-darker-blue dark:text-white">
        <img :src="currentCountryDetails[0].flags.png" alt="" class="flag-img" />
        <div>
            <h2 class="country-name">
                {{ capitalize(countryName) }}
            </h2>
            <p v-for="(detail, key) in countryDetails" :key="key" class="detail-list font-semibold">
                <span v-if="detail" class="font-bold">{{ capitalize(key.replace(/([A-Z])/g, ' $1').trim()) }}: </span>
                <span class="detail-text font-normal">{{ detail }}</span>
            </p>
            <p v-if="borders" class="border-countries">
                <span class="border-text font-semibold">Border Countries:</span>
                <span
                    v-for="(border, key) in borders"
                    :key="key"
                    class="border-list m-1 bg-white p-2 text-xs shadow dark:bg-dark-blue dark:text-white"
                >
                    {{ border }}
                </span>
            </p>
        </div>
    </div>
</template>

<style>
/********** Back-button **********/
.back-btn {
    display: flex;
    width: 100px;
    height: 2.5rem;
    border-radius: 5px;
    box-shadow: 0 0 6px rgba(0, 0, 0, 0.2);
    align-items: center;
    margin: 2rem;
    padding-left: -1.2rem;
}

.back-btn:hover {
    opacity: 80%;
}

.btn-container {
    align-items: center;
    justify-content: center;
}

.arrow {
    margin-right: 5px;
}

/********** Details **********/
.details {
    display: flex;
    max-height: 100%;
    flex-wrap: wrap;
    justify-content: space-evenly;
    align-content: center;
    padding: 20px;
}

.flag-img {
    width: 100%;
    height: auto;
    margin: 20px;
}

.country-name {
    padding: 20px;
    text-align: center;
    font-size: 36px;
    font-weight: bold;
}

.detail-list {
    padding: 5px;
    text-align: center;
    font-size: 16px;
}

.border-countries {
    padding: 10px;
}

@media (min-width: 768px) {
    .details {
        display: grid;
        align-items: center;
        grid-template-columns: 1fr 1fr;
        padding: 20px;
    }

    .flag-img {
        padding-left: 10%;
    }

    .country-name {
        padding: 20px;
        text-align: center;
    }

    .detail-list {
        display: grid;
        grid-template-columns: repeat(2, 1fr);
        text-align: left;
        margin-left: 80px;
    }

    .border-countries {
        margin-left: 75px;
    }
}
</style>

<script setup>
import { inject } from 'vue'
import capitalize from 'lodash.capitalize'
import router from '../router'
import Icon from '../components/Icon.vue'

const countries = inject('countries')

const countryName = router.currentRoute.value.params.countryName

const currentCountryDetails = countries._rawValue.filter((country) => country.name.common.toLowerCase() === countryName)

const currentCountry = currentCountryDetails[0]
const borders = currentCountry?.borders

const countryDetails = {
    nativeName: currentCountry?.altSpellings[1],
    population: currentCountry?.population.toLocaleString(),
    region: currentCountry?.region,
    subRegion: currentCountry?.subregion,
    capital: currentCountry?.capital?.[0],
    topLevelDomain: currentCountry?.tld?.[0],
    currencies: Object.keys(currentCountry?.currencies).join(', '),
    languages: Object.values(currentCountry?.languages).join(', '),
}

const returnHome = () => {
    router.push({ path: '/' })
}
</script>
