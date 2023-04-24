<template>
    <div class="flex flex-col">
        <h5
            class="mb-10 text-2xl font-bold tracking-tight text-gray-900 dark:text-white text-center"
        >
            Black and co calculator
        </h5>
        <div class="flex flex-row justify-center">
            <Card class="mr-6">
                <div class="flex flex-col">
                    <div class="mb-6 flex flex-col">
                        <b
                            class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
                        >
                            Gender
                        </b>
                        <div class="flex">
                            <div class="flex mr-6">
                                <label class="text-white mr-2">Man</label>
                                <input
                                    type="radio"
                                    :value="0"
                                    v-model.number="gender"
                                />
                            </div>
                            <div class="flex">
                                <label class="text-white mr-2">Woman</label>
                                <input
                                    type="radio"
                                    :value="1"
                                    v-model.number="gender"
                                />
                            </div>
                        </div>
                    </div>
                    <BaseInput
                        v-model.number="weight"
                        label="Weight (Kilograms Kg)"
                    />
                    <BaseInput
                        v-model.number="height"
                        label="Height (Meters m)"
                    />
                    <BaseInput
                        v-model.number="age"
                        label="Age"
                    />

                    <div class="mb-6">
                        <label
                            for="metabolism"
                            class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
                            >Base metabolism (Kcal)</label
                        >
                        <input
                            type="metabolism"
                            :value="Math.round(baseMetabolism as number)"
                            id="metabolism"
                            class="disabled:opacity-50 bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                            disabled
                        />
                    </div>
                </div>
            </Card>

            <Card>
                <div class="flex flex-col">
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
                        />
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
                        />
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
                        />
                    </div>

                    <div class="mb-6">
                        <label
                            for="slowWalking"
                            class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
                        >
                            {{
                                gender === 0
                                    ? 'Slow walking time'
                                    : 'Fast walking time'
                            }}
                        </label>
                        <input
                            type="text"
                            v-model.number="slowWalking"
                            id="slowWalking"
                            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                            placeholder="Enter your slow walking time here..."
                        />
                    </div>

                    <div
                        v-show="gender === 0"
                        class="mb-6"
                    >
                        <label
                            for="fastWalking"
                            class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
                            >Fast walking time</label
                        >
                        <input
                            type="text"
                            v-model.number="fastWalking"
                            id="fastWalking"
                            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                            placeholder="Enter your fast walking time here..."
                        />
                    </div>

                    <div class="mb-6">
                        <label
                            for="highIntensity"
                            class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
                            >High intensity sport</label
                        >
                        <input
                            type="text"
                            v-model.number="highIntensity"
                            id="highIntensity"
                            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                            placeholder="Enter your high intensity sport time here..."
                        />
                    </div>

                    <div class="mb-6">
                        <label
                            for="total"
                            class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
                            >Sum of hours (Need to be 24)</label
                        >
                        <input
                            type="text"
                            :value="totalOfHours"
                            id="total"
                            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                            disabled
                        />
                    </div>
                </div>
            </Card>
        </div>
    </div>
</template>

<script setup lang="ts">
import Card from '~/components/UI/Card.vue'
import BaseInput from '~/components/UI/BaseInput.vue'
import isNumber from 'lodash-es/isNumber'

// Base Metabolism
const gender = ref<number>(0)
const weight = ref<number>(0)
const height = ref<number>(0)
const age = ref<number>(0)

const isBaseMetabolismValid = computed(() => {
    return (
        isNumber(weight.value) &&
        weight.value > 0 &&
        isNumber(age.value) &&
        age.value > 0 &&
        isNumber(height.value) &&
        height.value > 0
    )
})

const baseMetabolism = computed(() => {
    if (!isBaseMetabolismValid.value) return 0
    const factor = gender.value ? 0.963 : 1.083
    return (
        (factor *
            Math.pow(weight.value as number, 0.48) *
            Math.pow(height.value as number, 0.5) *
            Math.pow(age.value as number, -0.13) *
            1000) /
        4.18
    )
})

// NAP
const sleep = ref<number | null>(0)
const sitting = ref<number | null>(0)
const standing = ref<number | null>(0)
const slowWalking = ref<number | null>(0)
const fastWalking = ref<number | null>(0)
const highIntensity = ref<number | null>(0)

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

const totalOfHours = computed(() => {
    if (!valuesAreValid.value) return 0
    const sum = ((((((((((sleep.value as number) + sitting.value) as number) +
        standing.value) as number) + slowWalking.value) as number) +
        fastWalking.value) as number) + highIntensity.value) as number

    if (sum > 24 || sum < 0) return 'Error : Need to be between 0 and 24'

    return sum
})
</script>
