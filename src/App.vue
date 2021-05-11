<template>
	<div id="app">
		<!-- HEADER -->
		<SearchMovie @getFilm="getFilm" />

		<!-- MAIN -->
		<main>
			<section class="movie-details">
				<div class="info">
					<h1>{{ this.clickedMovie.title ? this.clickedMovie.title : this.clickedMovie.name }}</h1>
					<span v-if="searchTrigger"
						>Release date:
						{{
							this.clickedMovie.release_date ? this.clickedMovie.release_date : this.clickedMovie.first_air_date
						}}</span
					>
					<span v-if="searchTrigger">Average {{ this.clickedMovie.vote_average }}</span>
					<p>
						{{ overview != '' ? this.clickedMovie.overview : 'nessuna descrizione' }}
					</p>
				</div>
				<div
					class="bigBG"
					:style="{
						backgroundImage: `linear-gradient(to left, rgba(255, 255, 255, 0) 0%, rgb(132, 23, 23) 80%), url(https://image.tmdb.org/t/p/w1280${this.clickedMovie.poster_path})`,
					}"
				></div>
			</section>
			<section class="search-result">
				<FilmList :filmList="filmsResult" :searchTrigger="searchTrigger" @getInfo="getInfo" />
				<TvSeriesList :seriesList="tvSeriesResult" :searchTrigger="searchTrigger" @getInfo="getInfo" />
			</section>
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
				clickedMovie: {},
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
				console.log(this.clickedMovie);
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

	.movie-details {
		display: flex;
		height: 500px;
	}

	.info {
		width: 40%;
	}

	.bigBG {
		height: 500px;
		background-size: cover;
		position: absolute;
		right: 0px;
		top: 0;
		width: 60%;
		background-position-y: 50%;
	}
</style>
