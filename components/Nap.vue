<template>
    <Card>
        <form @submit.prevent="submitHandler" class="mt-5 flex flex-col">
            <div class="mb-6">
                <label
                    for="sleep"
                    class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
                    >Sleep time</label
                >
                <input
                    type="text"
                    id="sleep"
                    v-model.number="sleep"
                    class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                    placeholder="Enter your sleep time here..."
                    required />
            </div>

            <div class="mb-6">
                <label
                    for="height"
                    class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
                    >Sitting time</label
                >
                <input
                    type="text"
                    id="sitting"
                    v-model.number="sitting"
                    class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                    placeholder="Enter your sitting time here..."
                    required />
            </div>

            <div class="mb-6">
                <label
                    for="standing"
                    class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
                    >Standing time</label
                >
                <input
                    type="text"
                    v-model.number="standing"
                    id="standing"
                    class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                    placeholder="Enter your standing time here..."
                    required />
            </div>

            <div class="mb-6">
                <label
                    for="slowWalking"
                    class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
                    >Slow walking time</label
                >
                <input
                    type="text"
                    v-model.number="slowWalking"
                    id="slowWalking"
                    class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                    placeholder="Enter your slow walking time here..."
                    required />
            </div>

            <div class="mb-6">
                <label
                    for="slowWalking"
                    class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
                    >Slow walking time</label
                >
                <input
                    type="text"
                    v-model.number="slowWalking"
                    id="slowWalking"
                    class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                    placeholder="Enter your slow walking time here..."
                    required />
            </div>


            <button
                :disabled="!valuesAreValid"
                type="submit"
                class="disabled:opacity-25 text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm w-full sm:w-auto px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800"
                >Calculate base metabolism</button
            >
        </form>
    </Card>
</template>

<script setup lang="ts">
    import Card from './UI/Card.vue';
    import isNumber from 'lodash-es/isNumber'
    const sleep = ref<number | null>(null)
    const sitting = ref<number | null>(null)
    const standing = ref<number | null>(null)
    const slowWalking = ref<number | null>(null)
    const fastWalking = ref<number | null>(null)
    const highIntensity = ref<number | null>(null)

    const emit = defineEmits<{
        (e: 'update:nap', value: number): void
    }>()

    const nap = ref<number | null>(null)

    const valuesAreValid = computed<boolean>(() => {
        return (
            isNumber(sleep.value) &&
            isNumber(sitting.value) &&
            isNumber(standing.value) &&
            isNumber(slowWalking.value) &&
            isNumber(fastWalking.value) &&
            isNumber(highIntensity.value)
        )
    })

    const submitHandler = () => {
        if (!valuesAreValid) return
        nap.value =
            (sleep.value as number) * 1 +
            (sitting.value as number) * 1.5 +
            (standing.value as number) * 2.2 +
            (slowWalking.value as number) * 3 +
            (fastWalking.value as number) * 3.5 +
            (highIntensity.value as number) * 5

        emit('update:nap', nap.value)
    }
</script>
