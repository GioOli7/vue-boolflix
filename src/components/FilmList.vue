<template>
	<section class="film-list">
		<span v-show="filmList.length == 0 && searchTrigger == true">Non ci sono risultati</span>
		<div
			class="film-item"
			v-for="(film, index) in filmList"
			:key="index"
			v-on:click="$emit('getInfo', film)"
			:style="{
				backgroundImage: `url(https://image.tmdb.org/t/p/w342${film.poster_path})`,
			}"
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
