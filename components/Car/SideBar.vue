<script setup>
const { makes } = useCars();
const modal = ref({
    make: false,
    location: false,
    price: false
});

const priceRange = ref({
    min: "",
    max: ""
});

const city = ref("");
const route = useRoute();
const router = useRouter();

const priceRangeText = computed(() => {
    const minPrice = route.query.minPrice;
    const maxPrice = route.query.maxPrice;
    if (!minPrice && !maxPrice) {
        return "Any"
    } else if (!minPrice && maxPrice) {
        reurn`< $${maxPrice}`
    } else if (minPrice && !maxPrice) {
        return `> $${minPrice}`
    } else {
        return `$${minPrice}-$${maxPrice}`
    }
});

const updateModal = (key) => {
    for (const modalKey in modal.value) {
        if (modalKey === key) {
            modal.value[modalKey] = !modal.value[modalKey];
        } else {
            modal.value[modalKey] = false;
        }
    }
};

const onChangeLocation = () => {
    updateModal("location");
    if (!city.value) return;

    if (!isNaN(parseInt(city.value))) {
        throw createError({
            statusCode: 400,
            message: "City name must be a string"
        })
    }

    navigateTo(`/city/${city.value}/car/${route.params.make}`);
    city.value = "";
}

const onChangeMake = (make) => {
    updateModal(make);
    navigateTo(`/city/${route.params.city}/car/${make}`);
}

const onChangePrice = () => {
    updateModal('price');
    if (priceRange.value.max && priceRange.value.min) {
        if (priceRange.value.min > priceRange.value.max) return;
    }
    router.push({
        query: {
            minPrice: priceRange.value.min,
            maxPrice: priceRange.value.max
        }
    })
}
</script>
<template>
    <div class="shadow border w-64 mr-10 z-30 h-[190px]">
        <div class="p-5 flex justify-between relative cursor-pointer border-b">
            <h3>Location</h3>
            <h3
                @click="updateModal('location')"
                class="text-blue-400 capitalize"
            >
                {{ route.params.city }}
            </h3>
            <div
                v-if="modal.location"
                class="absolute border shadow left-40 p-5 top-1 -m-1 bg-white"
            >
                <input
                    v-model="city"
                    class="border padding-1 rounded"
                    type="text"
                >
                <button
                    @click="onChangeLocation"
                    class="bg-blue-400 w-full mt-2 rounded text-white p-1"
                >
                    Apply
                </button>
            </div>
        </div>

        <div class="p-5 flex justify-between relative cursor-pointer border-b">
            <h3>Make</h3>
            <h3
                @click="updateModal('make')"
                class="text-blue-400 capitalize"
            >
                {{ route.params.make || 'Any' }}
            </h3>
            <div
                v-if="modal.make"
                class="absolute border shadow left-40 p-5 top-1 -m-1 w-[600px] flex justify-between flex-wrap bg-white"
            >
                <h4
                    v-for="(make, index) in makes"
                    @click="onChangeMake(make)"
                    :key="index"
                    class="w-1/3"
                >
                    {{ make }}
                </h4>
            </div>
        </div>

        <div class="p-5 flex justify-between relative cursor-pointer border-b">
            <h3>Price</h3>
            <h3
                @click="updateModal('price')"
                class="text-blue-400 capitalize"
            >
                {{ priceRangeText }}
            </h3>
            <div
                v-if="modal.price"
                class="absolute border shadow left-40 p-5 top-1 -m-1 bg-white"
            >
                <input
                    class="border p-1 rounded"
                    type="number"
                    placeholder="Min"
                    min="0"
                    v-model="priceRange.min"
                >
                <input
                    class="border p-1 rounded"
                    type="number"
                    placeholder="Max"
                    min="0"
                    v-model="priceRange.max"
                >
                <button
                    @click=onChangePrice()
                    class="bg-blue-400 w-full mt-2 rounded text-white p-1"
                >
                    Apply
                </button>
            </div>
        </div>
    </div>
</template>