<template>
    <form @submit.prevent="submitHandler" class="mt-5 flex flex-col">
        <div class="mb-6">
            <label
                for="weight"
                class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
                >Weight (Kg)</label
            >
            <input
                type="text"
                id="weight"
                v-model.number="weight"
                class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                placeholder="Enter your weight here..."
                required />
        </div>
        <div class="mb-6">
            <label
                for="height"
                class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
                >Height (m)</label
            >
            <input
                type="text"
                id="height"
                v-model.number="height"
                class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                placeholder="Enter your height here..."
                required />
        </div>
        <div class="mb-6">
            <label
                for="age"
                class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
                >Age</label
            >
            <input
                type="text"
                v-model.number="age"
                id="confirm_password"
                class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                placeholder="Enter your age here..."
                required />
        </div>

        <div v-if="baseMetabolism !== null" class="mb-6">
            <label
                for="metabolism"
                class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
                >Base metabolism</label
            >
            <input
                type="metabolism"
                v-model.number="baseMetabolism"
                id="metabolism"
                class="disabled:opacity-50 bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                disabled />
        </div>

        <button
            :disabled="!valuesAreValid"
            type="submit"
            class="disabled:opacity-25 text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm w-full sm:w-auto px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800"
            >Calculate base metabolism</button
        >
    </form>
</template>

<script setup lang="ts">
    import isNumber from 'lodash-es/isNumber'
    const weight = ref<number | null>(null)
    const height = ref<number | null>(null)
    const age = ref<number | null>(null)

    const emit = defineEmits<{
        (e: 'update:baseMetabolism', value: string): void
    }>()

    const baseMetabolism = ref<number | null>(null)

    const valuesAreValid = computed<boolean>(() => {
        return (
            isNumber(weight.value) &&
            isNumber(height.value) &&
            isNumber(age.value)
        )
    })

    const submitHandler = () => {
        if (!valuesAreValid) return
        baseMetabolism.value =
            (1.083 *
                Math.pow(weight.value as number, 0.48) *
                Math.pow(height.value as number, 0.5) *
                Math.pow(age.value as number, -0.13) *
                1000) /
            4.18
    }
</script>
