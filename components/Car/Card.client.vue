<script setup>
import heartFilled from "@/assets/heartFilled.png"
import heartOutline from "@/assets/heartOutline.png"
const props = defineProps({
    car: {
        type: Object,
        required: true
    },
    favored: {
        type: Boolean
    }
});

const emit = defineEmits(['favoriteCar']);
</script>

<template>
    {{ favored }}
    <div class="relative shadow border w-full overflow-hidden mb-5 h-[200px]">
        <img
            class="absolute w-7 right-5 top-2 z-20 cursor-pointer"
            :src="favored ? heartFilled : heartOutline"
            alt=""
            @click="emit('favoriteCar', car.id)"
        >
        <div class="flex h-full">
            <NuxtImg
                @click="navigateTo(`/car/${car.name}-${car.id}`)"
                class="w-[300px] h-full object-contain cursor-pointer"
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
    </div>
</template>