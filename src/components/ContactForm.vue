<template>
	<div class="flex flex-col gap-4">
		<base-input v-model="contact.name" placeholder="Имя" :error="errors.name" />
		<base-input
			v-model="contact.phone"
			placeholder="Телефон +7 (XXX) XXX-XX-XX"
			:error="errors.phone"
			mask="+7 (###) ###-##-##"
		/>
		<base-input
			v-model="contact.email"
			placeholder="E-mail"
			:error="errors.email"
		/>
		<base-button @click="onSubmit">
			{{ hasEdit ? 'Сохранить' : 'Добавить' }} контакт
		</base-button>
	</div>
</template>

<script setup lang="ts">
import BaseButton from '@/components/base/BaseButton.vue'
import BaseInput from '@/components/base/BaseInput.vue'
import { defineProps, onMounted, ref } from 'vue'
import { nanoid } from 'nanoid'
import * as yup from 'yup'

const props = defineProps<{
	contact?: IContact
	hasEdit?: boolean
}>()

const contact = ref<IContact>({
	id: nanoid(),
	name: '',
	phone: '',
	email: '',
})

const errors = ref<Record<string, string>>({})

const emit = defineEmits<{
	(event: 'addContact', contact: IContact): void
	(event: 'editContact', contact: IContact): void
}>()

const schema = yup.object({
	name: yup.string().required('Имя обязательно'),
	phone: yup.string().required('Телефон обязателен'),
	email: yup
		.string()
		.email('Некорректный e-mail')
		.required('E-mail обязателен'),
})

const onSubmit = () => {
	schema
		.validate(contact.value, { abortEarly: false })
		.then(() => {
			if (props.hasEdit) {
				emit('editContact', contact.value)
			} else {
				emit('addContact', contact.value)
			}
		})
		.catch((err) => {
			if (err instanceof yup.ValidationError) {
				errors.value = { name: '', phone: '', email: '' }
				err.inner.forEach((error) => {
					if (error.path) {
						errors.value[error.path] = error.message
					}
				})
			}
		})
}

onMounted(() => {
	if (props.contact) {
		contact.value = { ...props.contact }
	}
})
</script>
