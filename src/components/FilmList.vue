<template>
	<section class="film-list">
		<h2>Film</h2>
		<div class="film-item" v-for="(film, index) in filmList" :key="index">
			<FilmItem :details="filmList[index]" />
		</div>
		<span v-show="filmList.length == 0 && searchTrigger == true">Non ci sono risultati</span>
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

<style></style>
