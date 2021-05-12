<template>
	<div id="app">
		<!-- HEADER -->
		<Header @getFilm="getFilm" />

		<!-- TODO ottimizzare questa sezione -->
		<!-- MAIN -->
		<main>
			<Hero :movie="clickedMovie" />

			<section class="search-result" v-if="searchTrigger">
				<!-- film list -->
				<h2 class="list-type">Film</h2>
				<FilmList :filmList="filmsResult" :searchTrigger="searchTrigger" @getInfo="getInfo" />

				<!-- SerieTV list -->
				<h2 class="list-type">Serie tv</h2>
				<FilmList :filmList="tvSeriesResult" :searchTrigger="searchTrigger" @getInfo="getInfo" />
			</section>

			<section class="home-screen" v-show="homeLoaded" v-for="(list, index) in home" :key="'a' + index">
				<h2 class="list-type">{{ list.title }}</h2>
				<FilmList :filmList="list.movieList" @getInfo="getInfo" />
			</section>

			<LoadingScreen v-show="!homeLoaded" />
		</main>
	</div>
</template>

<script>
	import axios from 'axios';
	import Header from '@/components/Header';
	import Hero from '@/components/Hero';
	import FilmList from '@/components/FilmList';
	import LoadingScreen from '@/components/LoadingScreen';

	export default {
		name: 'App',
		components: {
			Header,
			Hero,
			FilmList,
			LoadingScreen,
		},
		created() {
			//
			this.getHomeData();
		},
		data() {
			return {
				apikey: '2b4a7028c4a25940b0c093d536ca98c6',
				home: [], //array di oggetti con all'interno le liste visualizzate al caricamento
				filmsResult: [], // film list from search
				tvSeriesResult: [], // tvSeries list from search
				searchTrigger: false,
				homeLoaded: false,
				clickedMovie: [], // clicked film's data
			};
		},
		methods: {
			getHomeData() {
				// Popular films
				axios
					.get(`https://api.themoviedb.org/3/movie/popular?api_key=${this.apikey}&language=it-IT&page=1`)
					.then(result => {
						this.home.push({
							title: 'Film - popular',
							movieList: result.data.results,
						});
					})
					.catch(error => console.log('error', error));
				// Upcoming films
				axios
					.get(`https://api.themoviedb.org/3/movie/upcoming?api_key=${this.apikey}&language=it-IT&page=1`)
					.then(result => {
						this.home.push({
							title: 'Film - upcoming',
							movieList: result.data.results,
						});
					})
					.catch(error => console.log('error', error));
				// Popular TVseries
				axios
					.get(`https://api.themoviedb.org/3/tv/popular?api_key=${this.apikey}&language=it-IT&page=1`)
					.then(result => {
						this.home.push({
							title: 'Serie TV - popular',
							movieList: result.data.results,
						});
					})
					.catch(error => console.log('error', error));
				setTimeout(() => {
					this.homeLoaded = true;
					console.log(this.liste);
				}, 1000);
			},

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
	@import '@/data/vars';
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
		background-color: $primary-color;
		display: flex;
		flex-direction: column;
		justify-content: space-between;
		padding: 20px;
	}

	.list-type {
		color: white;
		margin-bottom: 20px;
	}
</style>
