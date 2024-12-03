<script setup>
import { ref } from "vue"

const count = ref();
const countHex = ref();
const max = 200;
const colors = { color:"cyan", backgroundcolor:"black" };

</script>

<template>
    <h3>MyCounter Component</h3>
    Reactive integer-hex field: 
    <input type="text" v-integers-only.hexa.upper v-model="countHex" 
        v-focus:colors="colors" v-clearable/>
    <br/><br/>
    Entered value: <b>{{countHex}}</b>
    <br/><br/>    
    Reactive integer field: 
    <input type="text" v-integers-only v-model="count" v-max-value.bold="max"
        v-clearable/>
    <br/><br/>
    Max value: <b>{{max}}</b>
    <br/><br/>
    Entered value: <b>{{count}}</b>
    <br/><br/>
    <!-- It is <span v-timer /> -->
    <!-- <br>
    It is <span v-timer.ms /> more precisely -->
    Elapsed time <span v-timer.chrono />
    <br>
    Elapsed time <span v-timer.chrono.ms />more precisely
</template>