<template>
	<section class="film-list">
		<h2 class="list-type">{{ mainTitleList }}</h2>

		<div class="wrap">
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
		</div>
	</section>
</template>

<script>
	import FilmItem from '@/components/FilmItem';
	export default {
		name: 'FilmList',
		props: ['mainTitleList', 'filmList', 'searchTrigger'],
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

<style scoped lang="scss">
	.film-list {
		display: flex;
		flex-direction: column;
		// overflow-y: hidden;
		height: 250px;
		margin-bottom: 30px;
		position: relative;
		// CHROME scrollbar style
	}

	.wrap {
		display: flex;
		overflow-y: hidden;
		padding-bottom: 7px;
		scrollbar-width: thin;
		&::-webkit-scrollbar {
			background: rgba(0, 0, 0, 0.3);
			height: 8px;
		}
		&::-webkit-scrollbar-thumb {
			background: rgba(255, 255, 255, 0.3);
		}
		&::-webkit-scrollbar-thumb:hover {
			background: rgba(255, 255, 255, 0.5);
		}
	}

	.list-type {
		color: white;
		margin-bottom: 20px;
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
