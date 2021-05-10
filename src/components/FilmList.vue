<template>
	<section class="film-results">
		<h2>Film</h2>
		<div class="film-list">
			<div class="film-item" v-for="(film, index) in filmList" :key="index">
				<FilmItem :details="film" />
			</div>
		</div>
		<span v-show="filmList.length == 0 && searchTrigger == true">Non ci sono risultati</span>
	</section>
</template>

<script>
	import FilmItem from '@/components/FilmItem';
	export default {
		name: 'FilmList',
		props: ['filmList', 'searchTrigger'],
		components: {
			FilmItem,
		},
	};
</script>

<style scoped>
	.film-list {
		display: flex;
		overflow-y: hidden;
		scrollbar-width: thin;
	}

	.film-item {
		min-width: calc(100% / 6);
		height: 410px;
	}
</style>
