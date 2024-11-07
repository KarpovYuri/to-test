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
			<base-button color="red" @click="$emit('delete')"> Удалить </base-button>
			<base-button color="slate" @click="isShowModal = true">
				Редактировать
			</base-button>
		</div>
	</div>
	<base-modal v-if="isShowModal" @close="isShowModal = false">
		<contact-form
			:contact="contact"
			:hasEdit="true"
			@edit-contact="editContact"
		/>
	</base-modal>
</template>

<script setup lang="ts">
import type { PropType } from 'vue'
import { defineProps, ref } from 'vue'
import BaseButton from '@/components/base/BaseButton.vue'
import ContactForm from '@/components/ContactForm.vue'
import BaseModal from '@/components/base/BaseModal.vue'

const { contact } = defineProps({
	contact: {
		type: Object as PropType<IContact>,
		required: true,
	},
})

const isShowModal = ref(false)

const emit = defineEmits<{
	(event: 'editContact', contact: IContact): void
	(event: 'delete'): void
}>()

const editContact = (contact: IContact) => {
	emit('editContact', contact)
	isShowModal.value = false
}
</script>
