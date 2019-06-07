<template>
	<div class="game-container">
		<game-board :gameContent="cities" :coverImage="cityNight" gameTitle="Cities"/>
	</div>
</template>

<script>
	import { cities } from "../components/games/matching/data/card-content";
	import GameBoard from "../components/games/matching/GameBoard";
	import cityNight from "../assets/images/games/matching/cityNight.jpg";

	export default {
		data() {
			return {
				cityNight,
				cities
			};
		},
		components: {
			"game-board": GameBoard
		}
	};
</script>

<style>
</style>
