<script setup>
const props = defineProps({
    title: String,
    name: String,
    placeholder: String
})
const emits = defineEmits(['changeInput']);
const state = ref("");
const onChange = () => {
    emits("changeInput", state.value, props.name);
}
</script>

<template>
    <div class="flex flex-col w-[48%] t-2">
        <label
            for=""
            class="text-cyan-500 mb-2 text-sm"
        >
            {{ title }}
        </label>
        <input
            @input="onChange"
            v-model="state"
            :name="name"
            class="p-2 border w-100 rounded"
            :placeholder="placeholder"
        >
    </div>
</template>