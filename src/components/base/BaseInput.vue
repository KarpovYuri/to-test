<template>
	<div class="w-full">
		<input
			:value="inputValue"
			@input="onInput"
			class="text-black w-full outline-0 p-2 rounded-md"
			:class="{
				'outline outline-2 outline-red-500': error,
			}"
			type="text"
			:placeholder="placeholder"
		/>
		<p v-if="error" class="text-red-500 mt-2">{{ error }}</p>
	</div>
</template>

<script setup lang="ts">
import { watch, ref } from 'vue'

const props = defineProps({
	modelValue: {
		required: true,
	},
	error: {
		type: String,
		required: false,
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
