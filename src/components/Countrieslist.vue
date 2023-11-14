<script setup>
import { computed, ref } from 'vue';
import data from '../data.json';
import CardDetail from './CardDetail.vue';

const CountriesList = ref(data)
const seachCountry = ref('')
const Region = ref(['Africa','Americas','Asia','Europe','Oceania'])
const filterRegion = ref('')

const filteredCountries = computed(() => {
    if (filterRegion.value === '') {
        return CountriesList.value.filter((country) => country.name.toLowerCase().includes(seachCountry.value.toLowerCase()))
    } else {
        return CountriesList.value.filter((country) => country.region === filterRegion.value && country.name.toLowerCase().includes(seachCountry.value.toLowerCase()))
    }
})
const cardDetail = ref({})
const isCardDetail = ref(false)
const intoCardDetail = (item) => {
    isCardDetail.value = true
    cardDetail.value = item
    
}
const goBack = (value) => {
    isCardDetail.value = value
}
</script>
<template>
<card-detail v-if="isCardDetail" :cardDetail="cardDetail" @go-back="goBack"></card-detail>
<div v-else class="w-full bg-gray-100 text-[#1e2022] border-b-2 border-gray-100 drop-shadow-sm dark:drop-shadow-xl dark:bg-[#212c3d] dark:text-white" :class="{'h-screen' :filteredCountries.length <= 4 }">
    <div class="px-12">
        <div class="md:flex justify-between py-4 md:py-8">
        <div class="flex">
            <input type="text" v-model="seachCountry"
                class="font-sans w-72 h-10 rounded-sm px-6 text-xs dark:bg-[#4a658d] placeholder:text-slate-400 placeholder:text-xs placeholder:ml-4" placeholder="Serach for a country...">
        </div>
        <select name="" id="" v-model="filterRegion" class="px-1 h-10 mt-2 font-sans w-36 rounded-sm text-sm  dark:bg-[#4a658d] bg-white ">
            <option value="">Filter by Rogion</option>
            <option :value="item" v-for="item in Region" >{{item}}</option>
        </select>
        </div>
        <transition>
        <div class="grid-cols-1 md:grid-cols-2 xl:grid-cols-4 grid gap-y-12  gap-x-3 h-full">
            <div class=" flex justify-center items-center cursor-pointer hover:scale-105" v-for="item in filteredCountries" :key="item.alpha3Code"  @click="intoCardDetail(item)">
                <div class=" rounded-md bg-gray-200 dark:bg-[#4a658d] md:h-[98%] xl:h-[95%] w-[80%] items-center">
                    <img :src="item.flags.png" alt="flags" class="h-[50%] w-full rounded-t-md">
                    <div class="p-4">
                        <div class="font-bold my-2 ">{{item.name}}</div>
                        <div class="xl:text-xs mb-1 xl:mb-3 text-white">
                            <span class="text-gray-500 dark:text-white">Population:</span>{{item.population}}
                        </div>
                        <div class="xl:text-xs mb-1 xl:mb-3 text-white">
                            <span class="text-gray-500 dark:text-white">Region:</span>{{item.region}}
                        </div>
                        <div class="xl:text-xs text-white">
                            <span class="text-gray-500 dark:text-white">Capital:</span> {{item.capital}}
                        </div>
                    </div>
                </div>
            </div>
        </div>
        </transition>
    </div>
</div>
</template>
