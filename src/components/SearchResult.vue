<template>
	<section class="search-result" v-if="searchTrigger">
		<div v-for="(list, index) in searchResults" :key="'a' + index">
			<FilmList :mainTitleList="list.title" :filmList="list.movieList" :searchTrigger="searchTrigger" @getInfo="getInfo" />
		</div>
	</section>
</template>

<script>
	import FilmList from '@/components/FilmList';

	export default {
		name: 'SearchResult',
		components: {
			FilmList,
		},
		props: ['searchResults', 'searchTrigger'],
		methods: {
			getInfo(obj) {
				this.$emit('getInfo', obj);
			},
		},
	};
</script>

<style></style>
