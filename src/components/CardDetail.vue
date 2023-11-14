<script setup>
import {computed, ref} from 'vue'
const emit = defineEmits(['go-back'])
const props = defineProps({
    cardDetail: Object
})

const { flags, name, nativeName, region, subregion, capital, topLevelDomain, currencies, languages, borders } = props.cardDetail;
const cardDetail = computed(() => {
    return {
        flags,
        name,
        nativeName,
        region,
        subregion,
        capital,
        topLevelDomain,
        currencies,
        languages,
        borders
    }
})
const goBack = ()=>{
    emit('go-back', false)
}
</script>
<template>
  <div class="w-full h-screen md:h-[92vh] bg-gray-100 text-[#1e2022] border-b-2 border-gray-100 drop-shadow-sm dark:drop-shadow-xl dark:bg-[#212c3d] dark:text-white">
   <div class="py-16 mx-12 ">
    <button @click="goBack()" class=" shadow-orange-50 border py-1  px-12 rounded border-black hover:bg-slate-100 hover:text-black" >Back</button>
   </div>
    <div class=" mx-12 grid grid-cols-1 xl:grid-cols-2 ">
       <div class="w-full flex justify-center items-center">
        <img :src="cardDetail.flags.png" class=" w-full md:w-[500px]">
       </div>
       <div class="p-2 ">
        <div class="text-xl font-sans font-bold mx-2 xl:mx-0 my-6">{{cardDetail.name}}</div>
        <div class="grid grid-cols-1 md:grid-cols-2 w-full mx-2 xl:mx-12">
            <div class="">
                <div class="mb-4">NativeName:{{cardDetail.nativeName}}</div>
                <div class="mb-4">Region:{{cardDetail.region}}</div>
                <div class="mb-4">SubRegion:{{cardDetail.subregion}}</div>
                <div class="">Capital:{{cardDetail.capital}}</div>
            </div>
            <div>
                <div class="mb-4">TopLevelDomain:{{cardDetail.topLevelDomain[0]}}</div>
                <div class="mb-4">Currencies:
                    <span v-for="(currency, index) in cardDetail.currencies" :key="index">
                        {{ currency.name }} ({{ currency.code }}){{ index !== cardDetail.currencies.length - 1 ? ', ' : '' }}
                    </span>
                </div>
                <div class="mb-4 flex flex-wrap">Languages:
                    <span v-for="(language, index) in cardDetail.languages" :key="index">
                        {{ language.name }} ({{ language.nativeName }}){{ index !== cardDetail.languages.length - 1 ? ', ' : '' }}
                    </span>
                </div>
            </div>
        </div>
        <div class="md:my-12 mx-2 xl:mx-0 flex flex-wrap text-center">
            <span class="my-auto text-md">Borders Countries:</span>
            <span class="border  border-gray-900 w-24 h-6 md:px-6 mb-1 mx-1 my-auto" v-for="(border, index) in cardDetail.borders" :key="index">
                {{ border }}{{ index !== cardDetail.borders.length - 1 ? '' : '' }}
            </span>
        </div>
    </div>
    </div>
    </div>
</template>

