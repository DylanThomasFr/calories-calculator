<template>
    <Card>
        <form @submit.prevent="submitHandler" class="mt-5 flex flex-col">
            <BaseInput v-model:modelValue="weight" label="Weight (Kg)" />
            <BaseInput v-model:modelValue="height" label="Height (m)" />
            <BaseInput v-model:modelValue="age" label="Age" />

            <div v-if="baseMetabolism !== null" class="mb-6">
                <label
                    for="metabolism"
                    class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
                    >Base metabolism</label
                >
                <input
                    type="metabolism"
                    :value="Math.round(baseMetabolism)"
                    id="metabolism"
                    class="disabled:opacity-50 bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                    disabled />
            </div>

            <button
                type="submit"
                class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm w-full sm:w-auto px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800"
                >Calculate base metabolism</button
            >
        </form>
    </Card>
</template>

<script setup lang="ts">
    import Card from '~/components/UI/Card.vue'
    import BaseInput from '../UI/BaseInput.vue'
    const weight = ref<number>(0)
    const height = ref<number>(0)
    const age = ref<number>(0)

    const emit = defineEmits<{
        (e: 'update:baseMetabolism', value: number): void
    }>()

    const baseMetabolism = ref<number | null>(null)

    const submitHandler = () => {
        baseMetabolism.value =
            (1.083 *
                Math.pow(weight.value as number, 0.48) *
                Math.pow(height.value as number, 0.5) *
                Math.pow(age.value as number, -0.13) *
                1000) /
            4.18
        emit('update:baseMetabolism', baseMetabolism.value)
    }
</script>
