<template></template>

<script setup lang="ts">
import Card from './UI/Card.vue'
import isNumber from 'lodash-es/isNumber'

const emit = defineEmits<{
    (e: 'update:nap', value: number): void
}>()

const nap = ref<number | null>(null)

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
