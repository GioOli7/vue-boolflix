<template>
	<section class="tvseries-results">
		<h2>Serie TV</h2>
		<div class="tvseries-list">
			<span v-show="seriesList.length == 0 && searchTrigger == true">Non ci sono risultati</span>
			<div
				class="film-item"
				v-for="(film, index) in seriesList"
				:key="index"
				v-on:click="$emit('getInfo', film)"
				:style="{
					backgroundImage: `url(https://image.tmdb.org/t/p/w342${film.poster_path})`,
				}"
			>
				<FilmItem :details="film" />
			</div>
		</div>
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
		height: 190px;
	}

	h2 {
		color: white;
		margin-bottom: 20px;
	}
</style>
