<template>
	<main class="flex flex-col gap-4">
		<base-button @click="isShowModal = true">Добавить контакт</base-button>
		<search-bar @search="search" />
		<div v-if="isLoading" class="text-center text-lg font-semibold">
			Загрузка...
		</div>
		<div
			v-else-if="filteredContacts.length === 0"
			class="text-center text-lg font-semibold"
		>
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
import { ref, computed, onMounted } from 'vue'

const isShowModal = ref(false)
const isLoading = ref(true)

const searchText = ref('')
const contacts = ref<IContact[]>([])

const filteredContacts = computed(() => {
	return contacts.value.filter((contact) =>
		contact.name.toLowerCase().includes(searchText.value.toLowerCase())
	)
})

const addContact = (contact: IContact) => {
	contacts.value.unshift(contact)
	localStorage.setItem('contacts', JSON.stringify(contacts.value))
	isShowModal.value = false
}

const deleteContact = (id: string) => {
	contacts.value = contacts.value.filter((contact) => contact.id !== id)
	localStorage.setItem('contacts', JSON.stringify(contacts.value))
}

const editContact = (contact: IContact) => {
	contacts.value = contacts.value.map((c) =>
		c.id === contact.id ? contact : c
	)
	localStorage.setItem('contacts', JSON.stringify(contacts.value))
}

const search = (text: string) => {
	searchText.value = text
}

onMounted(async () => {
	try {
		const savedContacts = localStorage.getItem('contacts')
		if (savedContacts) {
			contacts.value = JSON.parse(savedContacts)
			isLoading.value = false
			return
		}

		await new Promise((resolve) => setTimeout(resolve, 1500))

		const response = await fetch('/contacts.json')
		if (!response.ok) {
			throw new Error('Ошибка при загрузке данных')
		}

		contacts.value = await response.json()
		localStorage.setItem('contacts', JSON.stringify(contacts.value))
	} catch (error) {
		console.error(error)
	} finally {
		isLoading.value = false
	}
})
</script>
