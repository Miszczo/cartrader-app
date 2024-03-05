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
        features: '',
        description: '',
        image: null
    }
});

const onChangeInput = (data, name) => {
    info.value[name] = data;
}

const inputs = [
    {
        id: 1,
        title: "Model *",
        name: "model",
        placeholder: "Civic"
    },
    {
        id: 2,
        title: "Year *",
        name: "year",
        placeholder: "2019"
    },
    {
        id: 3,
        title: "Miles *",
        name: "miles",
        placeholder: "10000"
    },
    {
        id: 4,
        title: "City *",
        name: "city",
        placeholder: "Toronto"
    },
    {
        id: 5,
        title: "Number of Seats *",
        name: "seats",
        placeholder: "5"
    },
    {
        id: 6,
        title: "Features *",
        name: "features",
        placeholder: "Leather Interior, No Accidents"
    }
]
</script>

<template>
    <div class="mt-24">
        <h1 class="text-6xl">Create a new listing</h1>
    </div>
    <div class="shadow rounded p-3 mt-5 flex flex-wrap justify-between">
        <CarAdSelect
            @change-input="(data, name) => { onChangeInput(data, name) }"
            title="Make *"
            :options="makes"
            name="make"
        />
        <CarAdInput
            v-for="input in inputs"
            :key="input.id"
            @change-input="onChangeInput"
            :title="input.title"
            :name="input.name"
            :placeholder="input.placeholder"
        />
        <CarAdTextarea
            @change-input="onChangeInput"
            title="Description *"
            name="description"
        />
        <CarAdImage
        />
    </div>
</template>