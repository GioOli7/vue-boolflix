<template>
	<section class="movie-details" v-if="movie.title || movie.name">
		<div class="info">
			<!-- titolo film -->
			<h1 class="movie-title">{{ movie.title ? movie.title : movie.name }}</h1>

			<!-- subtitle con informazioni -->
			<div class="sub">
				<!-- release yer -->
				<div class="release">
					<span>Release Year</span>
					<!-- conditional necessario per evitare errori in console quando release date è null -->
					<span>{{
						movie.release_date
							? movie.release_date
								? movie.release_date.slice(0, 4)
								: movie.release_date
							: movie.first_air_date
							? movie.first_air_date.slice(0, 4)
							: movie.first_air_date
					}}</span>
				</div>
				<!-- average rating -->
				<div class="vote">
					<span>Rating avg</span>
					<span>{{ movie.vote_average }}</span>
				</div>
			</div>

			<!-- overview -->
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
	.movie-details {
		display: flex;
		height: 500px;
	}
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
			display: flex;
			flex-direction: column;
			align-items: center;
			margin-right: 10px;
			color: rgba(255, 255, 255, 0.5);
			background-color: rgba(0, 0, 0, 0.2);
			padding: 5px 10px;
		}
	}

	.sub {
		display: flex;
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
