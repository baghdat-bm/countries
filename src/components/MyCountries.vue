<script setup>
import { ref, onMounted, watch, inject } from "vue";

const names = ref([]); // Countries names displayed in the list
let countries = []; // All country names (retrieved only once at startup)
const name = inject("name");

async function getCountries() {
    var url = "https://restcountries.com/v3.1/all";
    var response = await fetch(url);
    var data = await response.text();
    countries = JSON.parse(data).map(function (elem) {
        return elem.name.common;
    });
    // In ascending alphabetical order
    countries = countries.sort((n1, n2) => {
        if (n1 > n2) return 1;
        if (n1 < n2) return -1;
        return 0;
    });
    return countries;
}

onMounted(async () => {
    names.value = await getCountries();
});

watch(name, () => {
    let countriesFiltered = countries.filter((n) => {
        const reg = new RegExp("^" + name.value, "i");
        if (n.match(reg)) return true;
        else return false;
    });
    names.value = countriesFiltered;
});

// watchEffect(() => {
//     console.log(props.name);
//     let countriesFiltered = countries.filter((n) => {
//         const reg = new RegExp("^" + props.name, "i");
//         if (n.match(reg)) return true;
//         else return false;
//     });
//     names.value = countriesFiltered;
// });

</script>

<template>
    <h3>Country List</h3>
    <div v-show="!countries.length">Fetching countries in progress...</div>
    Entered Country: {{ name }}
    <ul>
        <li v-for="n in names" :key="n">{{ n }}</li>
    </ul>
</template>