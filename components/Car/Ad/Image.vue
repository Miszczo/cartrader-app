<script setup>


const image = useState('carImage', () => {
    return {
        preview: null,
        image: null
    }
});

const emits = defineEmits(['changeInput']);
const onImageUpload = (event) => {
    const input = event.target;

    if (input.files) {
        const reader = new FileReader();

        console.log("reasasDatra");
        reader.readAsDataURL(input.files[0]);

        reader.onload = (e) => {
            console.log("ONLOAD", e)
            image.value.preview = e.target.result
        }

        image.value.image = input.files[0];
    }
    emits('changeInput', input.files[0], "image");
}
</script>

<template>
    <div class="col-md-5 offset-md-1 mt-2 w-[100%]">
        <form class="mt-2">
            <label
                for="fileInput"
                class="w-100 cursor-pointer block"
            >
                <span class="text-cyan-500 mb-2 text-sm">Image *</span>

                <div class="relative">
                    <input
                        @change="onImageUpload"
                        type="file"
                        accept="image/*"
                        id="fileInput"
                        class="hidden w-100 z-50"
                    >
                    <span>Browse File</span>
                </div>
            </label>
        </form>
        <pre>{{ image }}</pre>
        <div
            v-if="image.preview"
            class="border p-2 mt-3 w-56"
        >
            <img
                class="img-fluid"
                :src="image.preview"
            >
        </div>
    </div>
</template>
