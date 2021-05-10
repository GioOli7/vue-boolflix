<template>
	<div
		class="film-details"
		:style="{
			backgroundImage: `url(https://image.tmdb.org/t/p/w342${details.poster_path})`,
		}"
	>
		<!-- title -->
		<h3 class="title">{{ details.title ? details.title : details.name }}</h3>
		<!-- original title -->
		<h4 class="original-title">
			{{ details.original_title ? details.original_title : details.original_name }}
		</h4>
		<!-- if lang == it or en > show flags -->
		<div v-if="languages.includes(details.original_language)">
			<img :src="require(`@/images/${details.original_language}.png`)" :alt="details.title" />
		</div>
		<!-- else show text lang -->
		<h5 v-else>{{ details.original_language }}</h5>
		<!-- vote -->
		<div class="stars">
			<i class="fas fa-star" v-for="(star, index) in vote_average" :key="'a' + index"></i>
			<i class="far fa-star" v-for="(star, index) in empty_stars" :key="'b' + index"></i>
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
				vote_average: 0,
				empty_stars: 0,
			};
		},
		created() {
			this.voteStars();
		},
		methods: {
			voteStars() {
				this.vote_average = Math.ceil(this.details.vote_average / 2);
				this.empty_stars = 5 - this.vote_average;
			},
		},
	};
</script>

<style scoped lang="scss">
	img {
		width: 30px;
	}

	.film-details {
		background-size: cover;
		width: 100%;
		height: 100%;
	}

	.stars {
		color: gold;
	}
</style>
