<template>
	<section class="tvseries-list">
		<h2>Serie TV</h2>
		<div class="film-item" v-for="(film, index) in seriesList" :key="index">
			<FilmItem :details="seriesList[index]" />
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

<style></style>
