<template>
	<header>
		<div class="logo">
			<img :src="require(`@/assets/gioflix.png`)" alt="gioflix logo" />
		</div>
		<SearchMovie @getFilm="getFilm" />
	</header>
</template>

<script>
	import SearchMovie from '@/components/SearchMovie';
	export default {
		name: 'Header',
		components: {
			SearchMovie,
		},
		data() {
			return {};
		},
		methods: {
			getFilm(query) {
				this.$emit('getFilm', query);
			},
		},
	};
</script>

<style scoped lang="scss">
	header {
		display: flex;
		justify-content: space-between;
		align-items: center;
		padding: 10px 20px;
		background-color: rgb(10, 10, 10);
		.logo {
			img {
				max-width: 130px;
			}
		}
	}
</style>
