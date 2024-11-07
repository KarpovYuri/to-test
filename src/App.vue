<template>
	<main class="flex flex-col gap-4">
		<base-button>Добавить контакт</base-button>
		<search-bar @search="search()" />
		<contact-list :contacts="contacts" />
	</main>
</template>

<script setup lang="ts">
import BaseButton from '@/components/base/BaseButton.vue'
import SearchBar from '@/components/SearchBar.vue'
import ContactList from '@/components/ContactList.vue'

const search = () => {
	console.log('Search triggered')
}

const contacts = [
	{
		id: 1,
		name: 'Доцент',
		phone: '+7 (111) 111-11-11',
		email: 'alexander@example.com',
	},
	{
		id: 2,
		name: 'Хмырь',
		phone: '+7 (222) 222-22-22',
		email: 'gavrila@example.com',
	},
	{
		id: 3,
		name: 'Косой',
		phone: '+7 (333) 333-33-33',
		email: 'fedor@example.com',
	},
	{
		id: 4,
		name: 'Василий Алибабаевич',
		phone: '+7 (444) 444-44-44',
		email: 'vasiliy@example.com',
	},
]
</script>
