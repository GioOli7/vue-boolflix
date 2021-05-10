<template>
	<div id="app">
		<!-- HEADER -->
		<SearchMovie @getFilm="getFilm" />

		<!-- MAIN -->
		<main>
			<FilmList :filmList="filmsResult" />
		</main>
	</div>
</template>

<script>
	import axios from 'axios';
	import SearchMovie from '@/components/SearchMovie';
	import FilmList from '@/components/FilmList';

	export default {
		name: 'App',
		components: {
			SearchMovie,
			FilmList,
		},
		data() {
			return {
				apikey: '2b4a7028c4a25940b0c093d536ca98c6',
				filmsResult: [],
			};
		},
		methods: {
			getFilm(query) {
				this.filmsResult = [];
				const formatQuery = query
					.trim()
					.split(' ')
					.join('%20');
				// api request
				axios
					.get(
						`https://api.themoviedb.org/3/search/movie?api_key=${this.apikey}&language=it-IT&query=${formatQuery}&page=1&include_adult=false`
					)
					.then(result => {
						this.filmsResult = result.data.results;
						console.log(this.filmsResult);
					})
					.catch(error => {
						console.log('error', error);
					});
			},
		},
	};
</script>

<style lang="scss"></style>
