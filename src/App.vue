<template>
	<div id="app">
		<!-- HEADER -->
		<Header @getFilm="getFilm" />

		<!-- MAIN -->
		<main>
			<Hero :movie="clickedMovie" />
			<section class="search-result" v-if="searchTrigger">
				<FilmList :filmList="filmsResult" :searchTrigger="searchTrigger" @getInfo="getInfo" />
				<TvSeriesList :seriesList="tvSeriesResult" :searchTrigger="searchTrigger" @getInfo="getInfo" />
			</section>
		</main>
	</div>
</template>

<script>
	import axios from 'axios';
	import Header from '@/components/Header';
	import Hero from '@/components/Hero';
	import FilmList from '@/components/FilmList';
	import TvSeriesList from '@/components/TvSeriesList';

	export default {
		name: 'App',
		components: {
			Header,
			Hero,
			FilmList,
			TvSeriesList,
		},
		data() {
			return {
				apikey: '2b4a7028c4a25940b0c093d536ca98c6',
				filmsResult: [],
				tvSeriesResult: [],
				searchTrigger: false,
				clickedMovie: [],
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

			getInfo(obj) {
				this.clickedMovie = obj;
				// console.log(this.clickedMovie);
			},
		},
	};
</script>

<style lang="scss">
	* {
		margin: 0;
		padding: 0;
		box-sizing: border-box;
	}

	#app {
		display: flex;
		flex-direction: column;
		height: 100vh;
	}

	main {
		position: relative;
		flex-grow: 1;
		background-color: #841717;
		display: flex;
		flex-direction: column;
		justify-content: space-between;
		padding: 20px;
	}

	.film-item {
		min-width: 125px;
		max-width: 125px;
		height: 180px;
		margin-right: 5px;
		background-size: cover;
		background-position: center;
	}
</style>
