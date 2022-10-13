<template>
    <div>
        <h2>Country list</h2>
        <div class="columns">
            <div class="column is-two-fifths">
                <ul v-for="country in countries">
                    <li>
                        <router-link :to="{name:'details', params:{alpha3Code:country.alpha3Code}}">
                            <img class="flag"
                                :src="`https://flagpedia.net/data/flags/icon/72x54/${country.alpha2Code.toLowerCase()}.png`"
                                alt="">
                            <p>{{country.name.common}}</p>
                        </router-link>
                    </li>
                </ul>
            </div>
            <div class="column">
                <router-view></router-view>
            </div>

        </div>
        <div>
        </div>
    </div>

</template>



<script setup>
import { defineProps } from 'vue';
const props = defineProps(['countries'])

</script>

<style>
.flag {
    width: 100px;
    height: 80px;
}
</style>