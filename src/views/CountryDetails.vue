<template>
    <div v-if="countryInfo">
        <img :src="`https://flagcdn.com/w320/${countryInfo.alpha2Code.toLowerCase()}.png`"
            alt="country flag" class="flag"/>
        <h2>{{ countryInfo.name.common }}</h2>
        <ul>
            <li>
                <p>Capital</p>
                <p>{{ countryInfo.capital[0] }}</p>
            </li>
            <li>
                <p>Area</p>
                <p>{{ countryInfo.area }} km2</p>
            </li>
            <li>
                <h3>Borders</h3>
                <p v-if="countryInfo.borders.length === 0">This country has no borders</p>
                <div v-for="(border, index) in countryInfo.borders" :key="index">
                    <!-- <router-link :to="`/countries/${border}`">{{ border }}</router-link> -->
                    <router-link :to="{name:'details', params:{alpha3Code:border}}">{{ border }}</router-link>
                </div>
            </li>
        </ul>
    </div>
</template>
<script setup>
import { computed, onMounted, ref, watch, } from "vue";
import { useRoute } from 'vue-router';


// const alpha3Code = ref("");
const countryInfo = ref(undefined);
const route = useRoute();

const getCountryAlphaCode = async () => {
    // alpha3Code.value = route.params.alpha3Code;
    const res = await fetch(
        `https://ih-countries-api.herokuapp.com/countries/${route.params.alpha3Code}`
    );
    console.log(route.params.alpha3Code)
    const finalRes = await res.json();
    countryInfo.value = finalRes;
    console.log(countryInfo)
};


onMounted(() => {
    getCountryAlphaCode();
});

const countryCode = computed(() => {
    return route.params.alpha3Code
});

watch(countryCode, (newCountryCode) => {
    getCountryAlphaCode()
})

</script>

<style scoped>
.flag {
    width: 300px;
    height: auto;
}
</style>