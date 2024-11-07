<template>
	<div class="flex flex-col gap-4">
		<base-input v-model="contact.name" placeholder="Имя" />
		<base-input v-model="contact.phone" placeholder="Телефон" />
		<base-input v-model="contact.email" placeholder="E-mail" />
		<base-button @click="handleClick">
			{{ hasEdit ? 'Сохранить' : 'Добавить' }} контакт
		</base-button>
	</div>
</template>

<script setup lang="ts">
import BaseButton from '@/components/base/BaseButton.vue'
import BaseInput from '@/components/base/BaseInput.vue'
import { defineProps, onMounted, ref } from 'vue'
import { nanoid } from 'nanoid'

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

const emit = defineEmits<{
	(event: 'addContact', contact: IContact): void
	(event: 'editContact', contact: IContact): void
}>()

const handleClick = () => {
	if (props.hasEdit) {
		emit('editContact', contact.value)
	} else {
		emit('addContact', contact.value)
	}
}

onMounted(() => {
	if (props.contact) {
		contact.value = { ...props.contact }
	}
})
</script>
