<template>
	<main class="flex flex-col gap-4">
		<base-button @click="isShowModal = true">Добавить контакт</base-button>
		<search-bar @search="search" />
		<div v-if="contacts.length === 0" class="text-center text-lg font-semibold">
			Контакты не найдены
		</div>
		<contact-list
			v-else
			:contacts="filteredContacts"
			@delete="deleteContact"
			@edit-contact="editContact"
		/>
	</main>
	<base-modal v-if="isShowModal" @close="isShowModal = false">
		<contact-form @add-contact="addContact" />
	</base-modal>
</template>

<script setup lang="ts">
import BaseButton from '@/components/base/BaseButton.vue'
import SearchBar from '@/components/SearchBar.vue'
import ContactList from '@/components/ContactList.vue'
import BaseModal from '@/components/base/BaseModal.vue'
import ContactForm from '@/components/ContactForm.vue'
import { ref, computed } from 'vue'
import { nanoid } from 'nanoid'

const isShowModal = ref(false)
const contacts = ref([
	{
		id: nanoid(),
		name: 'Доцент',
		phone: '+7 (111) 111-11-11',
		email: 'alexander@example.com',
	},
	{
		id: nanoid(),
		name: 'Хмырь',
		phone: '+7 (222) 222-22-22',
		email: 'gavrila@example.com',
	},
	{
		id: nanoid(),
		name: 'Косой',
		phone: '+7 (333) 333-33-33',
		email: 'fedor@example.com',
	},
	{
		id: nanoid(),
		name: 'Василий Алибабаевич',
		phone: '+7 (444) 444-44-44',
		email: 'vasiliy@example.com',
	},
])

const searchText = ref('')

const filteredContacts = computed(() => {
	return contacts.value.filter((contact) =>
		contact.name.toLowerCase().includes(searchText.value.toLowerCase())
	)
})

const addContact = (contact: IContact) => {
	contacts.value.unshift(contact)
	isShowModal.value = false
}

const deleteContact = (id: string) => {
	contacts.value = contacts.value.filter((contact) => contact.id !== id)
}

const editContact = (contact: IContact) => {
	contacts.value = contacts.value.map((c) =>
		c.id === contact.id ? contact : c
	)
}

const search = (text: string) => {
	searchText.value = text
}
</script>
