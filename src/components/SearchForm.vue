<template>
    <form @submit.prevent="applyFilters" class="">
        <div class="my-4">
            <div class="flex justify-center">
                <button type="button" v-for="trip in tripItems" :key="trip" @click="activeTrip = trip"
                    class="text-sm border border-blue-900 border-solid px-2 py-0.5"
                    :class="activeTrip === trip ? 'bg-blue-900 text-white ' : ' text-black'">{{ trip }}</button>

            </div>
        </div>
        <div class="grid grid-cols-13 gap-x-2 py-2 border-b border-t border-blue-600">
            <input v-model="origin" class="border-2 border-solid px-1 border-gray-400 py-0.5 md:col-span-2" type="text"
                placeholder="From" />
            <input v-model="destination" class="border-2 border-solid px-1 border-gray-400 py-0.5 md:col-span-2" type="text"
                placeholder="To" />
            <input v-model="departureDate" class="border-2 border-solid px-1 border-gray-400 py-0.5 md:col-span-2"
                type="date" />
            <select v-model="dayMinus" class="border-2 border-solid px-1 border-gray-400 py-0.5 ">
                <option value=""> Day- </option>
                <option value="1">1</option>
                <option value="2">2</option>
                <option value="3">3</option>
                <option value="4">4</option>
                <option value="5">5</option>
            </select>
            <select v-model="dayPlus" class="border-2 border-solid px-1 border-gray-400 py-0.5">
                <option value=""> Day+ </option>
                <option value="1">1</option>
                <option value="2">2</option>
                <option value="3">3</option>
                <option value="4">4</option>
                <option value="5">5</option>
            </select>
            <select v-model="time" class="border-2 border-solid px-1 border-gray-400 py-0.5  md:col-span-2">
                <option value="anytime"> Anytime </option>
                <option value="00:00">00:00</option>
                <option value="01:00">01:00</option>
                <option value="02:00">02:00</option>
                <option value="03:00">03:00</option>
                <option value="04:00">04:00</option>
                <option value="05:00">05:00</option>
                <option value="06:00">06:00</option>
                <option value="07:00">07:00</option>
                <option value="08:00">08:00</option>
                <option value="09:00">09:00</option>
                <option value="10:00">10:00</option>
                <option value="11:00">11:00</option>
                <option value="12:00">12:00</option>
            </select>
            <div class="flex items-center space-x-2 justify-between md:col-span-3">
                <span class="w-1/5 text-center">
                    <PlusIcon class="block h-4 mx-auto w-6" aria-hidden="true" />
                </span>
                <select v-model="adt" class="border-2 border-solid px-1 w-2/5 border-gray-400 py-0.5">
                    <option value=""> ADT </option>
                </select>
                <select v-model="count" class="border-2 border-solid px-1 border-gray-400 py-0.5  w-2/5">
                    <option value=""> 1 </option>
                </select>
                <span class="w-1/5 text-center">
                    <PlusIcon class="block mx-auto h-4 w-6 text-black" aria-hidden="true" />
                </span>
            </div>
        </div>

        <div class="flex items-center justify-between border-b border-blue-600 py-2">
            <div class="flex items-center gap-x-1.5">
                <input id="push-everything" name="push-notifications" type="radio"
                    class="h-4 w-4 border-gray-300 text-indigo-600 focus:ring-indigo-600" />
                <label for="push-everything" class="block text-sm font-medium leading-6 text-gray-900">Extra Options</label>
            </div>
            <div class="space-x-6 flex items-center justify-between">
                <label for="push-email" class="block text-sm font-medium leading-6 text-gray-900">Environment</label>
                <div class="flex items-center gap-x-1.5">
                    <input id="push-everything" name="push-notifications" type="radio"
                        class="h-4 w-4 border-gray-300 text-indigo-600 focus:ring-indigo-600" />
                    <label for="push-everything" class="block text-sm font-medium leading-6 text-gray-900">Dummy</label>
                </div>
                <div class="flex items-center gap-x-1.5">
                    <input id="push-nothing" name="push-notifications" type="radio"
                        class="h-4 w-4 border-gray-300 text-indigo-600 focus:ring-indigo-600" />
                    <label for="push-nothing" class="block text-sm font-medium leading-6 text-gray-900">PDT</label>
                </div>
            </div>
            <div>
                <button type="submit"
                    class="bg-blue-900 text-sm font-medium uppercase text-white px-4 py-1.5 rounded">Search </button>
            </div>
        </div>
        <div v-if="isFilter">
            <p class="text-sm font-medium">Data parsed successfully</p>
        </div>
    </form>
</template>
<script setup>
import { PlusIcon } from '@heroicons/vue/24/outline';
import { ref, defineProps } from 'vue';

const props = defineProps(['filterData']);

const activeTrip = ref("One way");
const tripItems = ref(["Round trip", "One way", "Multi city"]);
const isFilter = ref(false);
const origin = ref('');
const destination = ref('');
const departureDate = ref('');
const dayMinus = ref('');
const dayPlus = ref('');
const time = ref('');
const adt = ref('');
const count = ref('');

const applyFilters = () => {
    // Gather all input values
    const inputData = {
        tripType: activeTrip.value,
        origin: origin.value,
        destination: destination.value,
        departureDate: departureDate.value,
        dayMinus: dayMinus.value,
        dayPlus: dayPlus.value,
        time: time.value,
        adt: adt.value,
        count: count.value
    };
    isFilter.value = true

    // Pass input data to the filterData function in the parent component
    props.filterData(inputData);
};
</script>