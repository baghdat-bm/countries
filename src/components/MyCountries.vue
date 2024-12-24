<script setup>


import {ref} from "vue";
import useFetchCountries from "@/composables/useFetchCountries";

const data = ref();
const url = "https://restcountries.com/v3.1/all";
const [startFetch] = useFetchCountries(url);
const initData = async () => {
  data.value = await startFetch();
}

</script>

<template>
  <button @click="initData">Start Fetch</button>
  <br><br>
  <b>Data</b> :
  <ul>
    <li v-for="(country, i) in data" :key="i">{{country}}</li>
  </ul>
</template>