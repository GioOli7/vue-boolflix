<template>
	<section class="film-list">
		<div class="film-item" v-for="(film, index) in filmList" :key="index">
			<FilmItem :details="filmList[index]" />
		</div>
	</section>
</template>

<script>
	import FilmItem from '@/components/FilmItem';
	export default {
		name: 'FilmList',
		props: ['filmList'],
		components: {
			FilmItem,
		},
	};
</script>

<style></style>
