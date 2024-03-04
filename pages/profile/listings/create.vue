<script setup>
definePageMeta({
    layout: 'custom'
});

const { makes } = useCars();

const info = useState('addInfo', () => {
    return {
        make: '',
        model: '',
        year: '',
        miles: '',
        price: '',
        city: '',
        seats: '',
        description: '',
        image: null
    }
});

const onChangeInput = (data, name) => {
    info.value[name] = data;
}
</script>

<template>
    <div class="mt-24">
        <h1 class="text-6xl">Create a new listing</h1>
    </div>
    {{ info.make }}
    <div class="shadow rounded p-3 mt-5 flex flex-wrap justify-between">
        <CarAdSelect
            @change-input="(state, name) => onChangeInput(state, name)"
            title="Make *"
            :options="makes"
            name="make"
        ></CarAdSelect>
    </div>
</template>