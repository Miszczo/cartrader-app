<script setup>
const props = defineProps({
    car: {
        type: Object,
        required: true
    }
})
</script>

<template>
    <div
        @click="navigateTo(`/car/${car.name}-${car.id}`)"
        class="shadow border w-full overflow-hidden mb-5 curson-pointer h-[200px]"
    >
        <div class="flex h-full">
            <img
                class="w-[300px] h-full object-contain"
                :src="car.url"
                :alt="car.name"
            />
            <div class="p-4 flex flex-col">
                <div>
                    <h2 class="text-2xl text-blue-700">{{ car.name }}</h2>
                    <p class="text-gray-700">
                        {{ car.description }}
                    </p>
                </div>
                <h3 class="mt-auto text-xl">{{ car.price }}</h3>
            </div>
        </div>
</div></template>