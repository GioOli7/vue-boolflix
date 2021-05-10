<template>
	<div class="film-details">
		<h2 class="title">{{ details.title }}</h2>
		<h4 class="original-title">{{ details.original_title }}</h4>
		<h4 class="lang">{{ details.original_language }}</h4>
		<h5 class="vote">{{ details.vote_average }}</h5>
	</div>
</template>

<script>
	export default {
		name: 'FilmItem',
		props: ['details'],
	};
</script>

<style></style>
