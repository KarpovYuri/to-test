<template>
	<input
		:value="inputValue"
		@input="onInput"
		class="text-black w-full outline-0 p-2 rounded-md"
		:class="{
			'outline outline-2 outline-red-500': hasError,
		}"
		type="text"
		:placeholder="placeholder"
	/>
</template>

<script setup lang="ts">
import { watch, ref } from 'vue'

const props = defineProps({
	modelValue: {
		required: true,
	},
	hasError: {
		type: Boolean,
		default: false,
	},
	placeholder: {
		type: String,
		default: 'Введите текст',
	},
})

const inputValue = ref(props.modelValue)

watch(
	() => props.modelValue,
	(newValue) => {
		inputValue.value = newValue
	}
)

const emit = defineEmits<{
	(event: 'update:modelValue', value: string): void
}>()

function onInput(event: Event) {
	const target = event.target as HTMLInputElement
	emit('update:modelValue', target.value)
}
</script>
