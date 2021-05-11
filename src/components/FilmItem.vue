<template>
	<div class="film-details">
		<!-- title -->
		<span class="title">Titolo: {{ details.title ? details.title : details.name }}</span>
		<!-- original title -->
		<span
			class="original-title"
			v-show="details.original_title != details.title || details.original_name != details.name"
		>
			Original title: {{ details.original_title ? details.original_title : details.original_name }}
		</span>
		<!-- if lang == it or en > show flags -->
		<div v-if="languages.includes(details.original_language)">
			<span>Lingua:</span>
			<img :src="require(`@/images/${details.original_language}.png`)" :alt="details.title" />
		</div>
		<!-- else show text lang -->
		<span v-else>Linga: {{ details.original_language }}</span>
		<!-- vote -->
		<!-- <span>Votazione:</span> -->
		<div class="stars">
			<i class="fas fa-star" v-for="(star, index) in Math.ceil(details.vote_average / 2)" :key="'c' + index"></i>
			<i class="far fa-star" v-for="(star, index) in 5 - Math.ceil(details.vote_average / 2)" :key="'d' + index"></i>
		</div>
	</div>
</template>

<script>
	export default {
		name: 'FilmItem',
		props: ['details'],
		data() {
			return {
				languages: ['en', 'it'],
			};
		},
		methods: {},
	};
</script>

<style scoped lang="scss">
	img {
		width: 30px;
	}

	.film-details {
		display: flex;
		flex-direction: column;
		justify-content: space-around;
		height: 100%;
		padding: 4px;
		color: white;
		text-align: center;
		background-color: rgba(0, 0, 0, 0.8);
		opacity: 0;
		transition: opacity 0.3s;
		font-size: 12px;
		&:hover {
			opacity: 1;
		}
	}

	.stars {
		color: gold;
	}
</style>
