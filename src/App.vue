<script setup>
import { ref } from 'vue';
import Header from './components/Header.vue';
import FlightTable from './components/FlightTable.vue';
import SearchForm from './components/SearchForm.vue';
import data from '../data.json';

// Define a reactive variable to hold the filtered flights
const filteredFlights = ref([]);

// Function to filter flight data based on the payload received from SearchForm
const filterData = (payload) => {
  console.log(payload);

  // Implement your filtering logic here
  // For example, filter flights based on payload
  // Update filteredFlights with the filtered data
  filteredFlights.value = data.flightOffer
  // .filter(flight => {
    // Implement your filtering logic based on payload
    // For example:
    // return flight.departure === payload.origin && flight.departure === payload.destination;
  // });
};
</script>

<template>
  <main class="">
    <Header/>
    <div class="border-b border-solid">
      <div class="mx-auto max-w-7xl px-2 sm:px-6 lg:px-8">
        <h2 class="text-xl font-bold text-gray-800">Master Price</h2>
      </div>
    </div>
    <div class="mx-auto max-w-7xl px-2 sm:px-6 lg:px-8 ">
      <!-- Pass the filterData function to the SearchForm component -->
      <SearchForm :filterData="filterData"/>
      
      <!-- Pass the filtered flights to the FlightTable component -->
      <FlightTable :flights="filteredFlights"/>
    </div>
  </main>
</template>