<template>
	<input
		type="text"
		v-model="query"
		v-on:keyup.enter="$emit('getFilm', query)"
		placeholder="Cerca un film"
	/>
</template>

<script>
	export default {
		name: 'SearchMovie',
		data() {
			return {
				query: '',
			};
		},
	};
</script>

<style scoped></style>
