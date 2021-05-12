<template>
	<div>
		<section class="home-screen" v-show="homeLoaded" v-for="(list, index) in home" :key="'b' + index">
			<FilmList :mainTitleList="list.title" :filmList="list.movieList" @getInfo="getInfo" />
		</section>
	</div>
</template>

<script>
	import FilmList from '@/components/FilmList';

	export default {
		name: 'TopFilmList',
		props: ['homeLoaded', 'home'],
		components: {
			FilmList,
		},
		methods: {
			getInfo(obj) {
				this.$emit('getInfo', obj);
			},
		},
	};
</script>

<style></style>
