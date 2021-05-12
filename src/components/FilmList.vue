<template>
	<section class="film-list">
		<span v-show="filmList.length == 0 && searchTrigger == true">Non ci sono risultati</span>
		<div
			class="film-item"
			v-for="(film, index) in filmList"
			:key="index"
			v-on:click="$emit('getInfo', film)"
			:style="{ backgroundImage: `url(${film.poster_path === null ? placeholder : baseIMGurl + film.poster_path})` }"
		>
			<FilmItem :details="film" />
		</div>
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
		data() {
			return {
				placeholder: require('@/assets/poster_placeholder.png'),
				baseIMGurl: 'https://image.tmdb.org/t/p/w342',
			};
		},
		methods: {},
	};
</script>

<style scoped>
	.film-list {
		display: flex;
		overflow-y: hidden;
		scrollbar-width: thin;
		height: 190px;
		margin-bottom: 30px;
	}

	.film-item {
		min-width: 125px;
		max-width: 125px;
		height: 180px;
		margin-right: 5px;
		background-size: cover;
		background-position: center;
		cursor: pointer;
	}
</style>
