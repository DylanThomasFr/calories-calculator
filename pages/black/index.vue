<template>
    <div class="flex flex-col">
        <h5 class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white text-center">
        Black and co calculator
    </h5>
    <div class="flex flex-row">
        <BaseMetabolism v-model:baseMetabolism="baseMetabolism"/>
        <Nap v-if="baseMetabolism !== null" />
    </div>
    </div>
    
    
</template>

<script setup lang="ts">
import BaseMetabolism from '~/components/black/BaseMetabolism'
import Nap from '~/components/Nap.vue'

const baseMetabolism = ref<number | null>(null)
</script>
