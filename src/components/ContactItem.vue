<template>
	<div
		class="flex flex-col sm:flex-row gap-3 sm:gap-6 justify-between items-center border border-slate-200 rounded-md p-3 border-dashed"
	>
		<ul class="w-full">
			<li><span class="opacity-50">Имя:</span> {{ contact.name }}</li>
			<li><span class="opacity-50">Телефон:</span> {{ contact.phone }}</li>
			<li><span class="opacity-50">E-mail:</span> {{ contact.email }}</li>
		</ul>
		<div class="flex flex-col gap-2 max-sm:w-full">
			<base-button color="red">Удалить</base-button>
			<base-button color="slate">Редактировать</base-button>
		</div>
	</div>
</template>

<script setup lang="ts">
import type { PropType } from 'vue'
import BaseButton from '@/components/base/BaseButton.vue'

const { contact } = defineProps({
	contact: {
		type: Object as PropType<IContact>,
		required: true,
	},
})
</script>
