<template>
	<section class="tvseries-results">
		<h2>Serie TV</h2>
		<div class="tvseries-list">
			<div class="film-item" v-for="(film, index) in seriesList" :key="index">
				<FilmItem :details="seriesList[index]" />
			</div>
		</div>
		<span v-show="seriesList.length == 0 && searchTrigger == true">Non ci sono risultati</span>
	</section>
</template>

<script>
	import FilmItem from '@/components/FilmItem';
	export default {
		name: 'TvSeriesList',
		props: ['seriesList', 'searchTrigger'],
		components: {
			FilmItem,
		},
	};
</script>

<style scoped>
	.tvseries-list {
		display: flex;
	}
</style>
