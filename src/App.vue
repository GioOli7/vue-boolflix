<template>
	<div id="app">
		<!-- HEADER -->
		<SearchMovie @getFilm="getFilm" />

		<!-- MAIN -->
		<main>
			<FilmList :filmList="filmsResult" :searchTrigger="searchTrigger" />
			<TvSeriesList :seriesList="tvSeriesResult" :searchTrigger="searchTrigger" />
		</main>
	</div>
</template>

<script>
	import axios from 'axios';
	import SearchMovie from '@/components/SearchMovie';
	import FilmList from '@/components/FilmList';
	import TvSeriesList from '@/components/TvSeriesList';

	export default {
		name: 'App',
		components: {
			SearchMovie,
			FilmList,
			TvSeriesList,
		},
		data() {
			return {
				apikey: '2b4a7028c4a25940b0c093d536ca98c6',
				filmsResult: [],
				tvSeriesResult: [],
				searchTrigger: false,
			};
		},
		methods: {
			getFilm(query) {
				this.filmsResult = [];
				this.tvSeriesResult = [];
				const formatQuery = query
					.trim()
					.split(' ')
					.join('%20');
				// Film Api request
				axios
					.get(
						`https://api.themoviedb.org/3/search/movie?api_key=${this.apikey}&language=it-IT&query=${formatQuery}&page=1&include_adult=false`
					)
					.then(result => (this.filmsResult = result.data.results))
					.catch(error => console.log('error', error));

				// Serie TV Api request
				axios
					.get(`https://api.themoviedb.org/3/search/tv?api_key=${this.apikey}&language=it-IT&query=${formatQuery}`)
					.then(result => (this.tvSeriesResult = result.data.results))
					.catch(error => console.log('error', error));
				// se non ci sono risultati ma non ho ancora fatto una ricerca, non lascio nessun feedback
				this.searchTrigger = true;
			},
		},
	};
</script>

<style lang="scss"></style>
