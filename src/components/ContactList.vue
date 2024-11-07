<template>
	<div class="flex flex-col gap-3">
		<contact-item
			v-for="contact in contacts"
			:key="`contact-${contact.id}`"
			:contact="contact"
		/>
	</div>
</template>

<script setup lang="ts">
import type { PropType } from 'vue'
import ContactItem from '@/components/ContactItem.vue'

const { contacts } = defineProps({
	contacts: {
		type: Array as PropType<IContact[]>,
		required: true,
	},
})
</script>
