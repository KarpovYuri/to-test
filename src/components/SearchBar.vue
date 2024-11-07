<template>
	<div class="flex gap-4">
		<base-input
			v-model="searchValue"
			@keydown.enter="$emit('search', searchValue)"
		/>
		<base-button color="purple" @click="$emit('search', searchValue)">
			Найти
		</base-button>
	</div>
</template>

<script setup lang="ts">
import BaseInput from '@/components/base/BaseInput.vue'
import BaseButton from '@/components/base/BaseButton.vue'
import { ref } from 'vue'

const searchValue = ref('')
</script>
