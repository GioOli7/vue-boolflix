<template>
	<header>
		<div class="logo">
			<img :src="require(`@/assets/gioflix.png`)" alt="gioflix logo" />
		</div>
		<input type="text" v-model="query" v-on:keyup.enter="$emit('getFilm', query)" placeholder="Cerca un film" />
	</header>
</template>

<script>
	export default {
		name: 'SearchMovie',
		data() {
			return {
				query: '',
			};
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
		input {
			height: 40px;
			width: 250px;
			background-color: rgb(10, 10, 10);
			color: #dc1a28;
			font-weight: bold;
			padding-left: 15px;
			border: 1px solid rgba(255, 255, 255, 0.1);
			outline: none;
			&:focus {
				border: 1px solid transparent;
				border-bottom: 1px solid #dc1a28;
			}
		}
	}
</style>
