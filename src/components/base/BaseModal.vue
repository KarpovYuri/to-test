<template>
	<teleport to="#app">
		<div
			class="absolute top-0 left-0 w-full h-full z-[1000] bg-black/50 flex items-center justify-center"
		>
			<div
				class="w-full sm:w-[500px] bg-gray-800 p-4 pt-10 rounded-lg relative"
			>
				<p
					class="absolute top-1 right-[10px] cursor-pointer font-bold"
					@click="$emit('close')"
				>
					X
				</p>
				<slot />
			</div>
		</div>
	</teleport>
</template>

<script setup lang="ts">
defineEmits(['close'])
</script>
