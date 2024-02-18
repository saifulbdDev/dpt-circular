<template>
  <div class="mt-8 flow-root">
    <div class="-mx-4 -my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
      <div class="inline-block min-w-full py-2 align-middle sm:px-6 lg:px-8">
        <table class="min-w-full divide-y divide-gray-300" v-if="flightOffers?.length">
          <thead>
            <tr class="bg-gray-300">
              <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">FLIGHT</th>
              <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">AIRCRAFT</th>
              <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">CLASS</th>
              <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">FARE</th>
              <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">ROUTE</th>
              <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">DEPARTURE</th>
              <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">ARRIVAL</th>
              <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">DURATION</th>
              <th scope="col" class="px-3 py-3.5 text-center text-sm font-semibold text-gray-900">PRICE</th>
            </tr>
          </thead>
          <tbody class="bg-white">
            <tr class="border-b border-red-600" v-for="(offer, index) in flightOffers" :key="index"
              :class="index % 2 === 0 ? '' : 'bg-gray-300'">
              <td class="whitespace-nowrap py-4 pl-4 pr-3 text-sm font-medium text-gray-900 sm:pl-3">
              
                <div v-for="(segment, j) in offer.segments" :key="j">


                  <p>{{ segment.carrierCode }}{{ segment.flightNumber }}</p>

                </div>
              </td>
              <td class="whitespace-nowrap py-4 pl-4 pr-3 text-sm font-medium text-gray-900 sm:pl-3">
          
                <p v-for="(segment, j) in offer.segments" :key="j">{{ segment.aircraft }}</p>


              </td>

              <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                <p v-for="(classItem, classKey) in offer.class[0]" :key="classKey">{{ classItem }}</p>
              </td>

              <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                <p v-for="(fareBasisItem, fareBasisKey) in offer.fareBasis[0]" :key="fareBasisKey">{{ fareBasisItem }}</p>
              </td>

             
              <td>
                <p v-for="(segment, j) in offer.segments" :key="j">{{ segment.arrival.iataCode }} - {{ segment.departure.iataCode }}</p>
              </td>
              <td>
                <p v-for="(segment, j) in offer.segments" :key="j">{{ segment.departure.at }}</p>
              </td>
              <td>
                <p v-for="(segment, j) in offer.segments" :key="j">{{ segment.arrival.at }}</p>
              </td>
              <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">{{ offer.itineraries[0].duration }}</td>
              <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500 flex flex-col justify-center items-center">
                <p>{{ offer.price }}</p>
                <button type="button"
                  class="bg-blue-900 text-sm font-medium uppercase text-white px-4 py-1.5 rounded">Select</button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>
<script setup>
import { computed } from "vue";
const props = defineProps({
  flights: Array,
});

const flightOffers = computed(() => {
  return props.flights.map(offer => ({
    ...offer,
    segments: offer?.itineraries[0]?.segments||[],
   
  }));
});


</script>