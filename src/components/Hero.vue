<template>
	<section class="movie-details" v-if="movie.title || movie.name">
		<div class="info">
			<h1 class="movie-title">{{ movie.title ? movie.title : movie.name }}</h1>
			<span class="release"> {{ movie.release_date ? movie.release_date : movie.first_air_date }}</span>
			<span class="vote">{{ movie.vote_average }}</span>
			<p class="overview">
				{{ movie.overview }}
			</p>
		</div>
		<div
			class="bigBG"
			:style="{
				backgroundImage: `linear-gradient(to left, rgba(255, 255, 255, 0) 0%, rgb(132, 23, 23) 80%), url(https://image.tmdb.org/t/p/original${movie.poster_path})`,
			}"
		></div>
	</section>
</template>

<script>
	export default {
		name: 'Hero',
		props: ['movie'],
	};
</script>

<style scoped lang="scss">
	.info {
		z-index: 1;
		position: relative;
		overflow-y: auto;
		width: 50%;
		padding-left: 40px;
		padding-right: 20px;
		max-height: 490px;
		scrollbar-width: none; //hide scrollbar in firefox
		-ms-overflow-style: none; /* IE and Edge */
		&::-webkit-scrollbar {
			//hide scrollbar in chrome, safari, opera
			display: none;
		}
		.movie-title {
			color: white;
			font-size: 60px;
			margin-bottom: 10px;
		}
		.overview {
			margin-top: 40px;
			color: white;
		}
		.vote,
		.release {
			margin-right: 10px;
			color: rgba(255, 255, 255, 0.5);
			background-color: rgba(0, 0, 0, 0.5);
			padding: 10px;
		}
	}

	.bigBG {
		height: 500px;
		background-size: cover;
		position: absolute;
		right: 0px;
		top: 0;
		width: 60%;
		background-position-y: 50%;
	}
</style>
