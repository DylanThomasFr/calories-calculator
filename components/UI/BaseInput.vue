<template>
    <div class="mb-6">
        <label
            class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
            >{{ props.label }}</label
        >
        <input
            type="text"
            :value="props.modelValue"
            @input="emit('update:modelValue', $event.target.value as string)"
            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
            placeholder="Enter your slow walking time here..."
            required
        />
    </div>
</template>

<script setup lang="ts">
const props = defineProps({
    modelValue: { type: [String, Number], required: true },
    label: { type: String, required: true },
})

const emit = defineEmits<{
    (e: 'update:modelValue', value: string | number): void
}>()
</script>
