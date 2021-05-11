<template>
	<section class="tvseries-results">
		<h2>Serie TV</h2>
		<div class="tvseries-list">
			<div
				class="film-item"
				v-for="(film, index) in seriesList"
				:key="index"
				:style="{
					backgroundImage: `url(https://image.tmdb.org/t/p/w342${film.poster_path})`,
				}"
			>
				<FilmItem :details="film" />
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
		overflow-y: hidden;
		scrollbar-width: thin;
	}

	.film-item {
		min-width: 200px;
		max-width: 200px;
		height: 300px;
		background-size: cover;
		background-position: center;
	}
</style>
