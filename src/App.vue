<template>
    <div>
        <Navbar />
        <div>
            <CountriesList :countries="countriesList" />
            <router-view></router-view>
        </div>
    </div>
</template>




<script setup>
import Navbar from './components/Navbar.vue';
import CountriesList from './views/CountriesList.vue'

import { ref } from 'vue'

const countriesList = ref(null);

const fetchCountries = async () => {
    const res = await fetch('https://ih-countries-api.herokuapp.com/countries');
    const finalResponse = await res.json();
    const sortedCountries = finalResponse.sort((a, b) => {
        return a.name.common.localeCompare(b.name.common)
    });
    countriesList.value = sortedCountries
};

fetchCountries();
</script>


<style scoped>

</style>
