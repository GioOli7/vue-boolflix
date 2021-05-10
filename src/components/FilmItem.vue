<template>
	<div class="film-details">
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
		<h5 class="vote">{{ details.vote_average }}</h5>
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
</style>
