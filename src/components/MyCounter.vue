<script setup>
import useGeolocationWithDetails from "../composables/useGeolocationWithDetails.js"
import useMap from "../composables/useMap.js"
import {onMounted, watchEffect} from "vue";

const [latitude, longitude, country, city] = useGeolocationWithDetails();
// The onMounted() method ensures that the "map" DOM element is correctly inserted into the DOM.
onMounted(() => {
  // The watchEffect() method waits for the latitude and longitude to be properly initialized.
  watchEffect(() => {
    if (latitude.value && longitude.value) useMap(latitude.value, longitude.value, "map");
  });
});
</script>

<template>
  <h3>MyCounter Component</h3>
  <p>Map around the city: <b v-show="city">{{ city }} - {{ country }}</b></p>
  <div id="map"/>
</template>

<style scoped>
#map {
  height: 300px;
  width: 100%;
}
</style>