<template>
	<div class="gamepiece-container">
		<transition name="flip" mode="in-out">
			<div class="cover" v-if="!clicked && !cardData.matched" @click="handleClick(cardData)">
				<img :src="coverImage" alt="panther face" class="cover-image">
			</div>
		</transition>

		<transition name="flip" mode="in-out">
			<!-- v-if="clicked && cardData.source !== '' && cardData.description !== ''" -->
			<div v-if="!cardData.matched && clicked" @click="handleClick(cardData)" class="game-piece">
				<img :src="cardData.source" :alt="cardData.name" class="images" v-if="cardData.source">
				<p v-if="cardData.description">{{cardData.description}}</p>
				<slot></slot>
			</div>
		</transition>
		<transition name="fade">
			<div v-if="cardData.matched " class="match image-container">
				<!-- <div class=""> -->
				<img :src="cardData.source" :alt="cardData.name" class="images" v-if="cardData.source">
				<p v-if="cardData.description">{{cardData.description}}</p>
				<!-- </div> -->
			</div>
		</transition>
	</div>
</template>

<script>
	export default {
		data: function() {
			return {
				id: "",
				clicked: false
			};
		},
		props: {
			cardData: {
				type: Object,
				required: true
			},
			firstSelected: {
				type: Object
			},
			resetClicked: {
				type: Boolean
			},
			clickCount: {
				type: Number
			},
			coverImage: {
				required: true
			}
		},
		watch: {
			resetClicked: function() {
				this.clicked = false;
			}
		},
		methods: {
			handleClick: function(val) {
				if (this.clickCount < 2) {
					this.clicked = !this.clicked;
					this.$emit("card-match-id", this.cardData);
				}
			}
		}
	};
</script>

<style lang="scss" scoped>
	$piece-height: 175px;
	$piece-width: 175px;
	.gamepiece-container {
		height: $piece-height;
		width: $piece-width;
		margin: 5px;
	}
	.game-piece {
		height: $piece-height;
		width: $piece-width;
		border-radius: 3px;
		background-color: #94aacc;
		display: flex;
		flex-direction: column;
		justify-content: center;
		text-align: center;
		margin: 5px;
		padding: 3px;
		box-sizing: border-box;
		cursor: pointer;
	}
	.match {
		margin: 5px;
		padding: 3px;
		height: $piece-height;
		width: $piece-width;
		box-sizing: border-box;
		border-radius: 3px;
		background-color: #6cbb5852;
		color: rgb(46, 61, 42);
		display: flex;
		flex-direction: column;
		justify-content: center;
		text-align: center;
		cursor: not-allowed;
	}
	.image-container {
		z-index: -1;
	}
	.cover {
		margin: 5px;
		padding: 3px;
		height: $piece-height;
		width: $piece-width;
		box-sizing: border-box;
		display: flex;
		flex-direction: column;
		justify-content: center;
		border-radius: 3px;
		background-color: #200202;
		cursor: pointer;
	}
	.cover-image {
		max-height: 95%;
		max-width: 95%;
		margin: auto;
	}
	.images {
		max-height: 95%;
		max-width: 95%;
		margin: auto;
	}
	.flip-enter-active {
		transition: all 0.35s cubic-bezier(0.55, 0.085, 0.68, 0.53); //ease-in-quad
		transform-style: preserve-3d;
	}
	.flip-leave-active {
		/* transition: all 2s cubic-bezier(0.25, 0.46, 0.45, 0.94); //ease-out-quad */
		display: none;
	}
	.flip-enter,
	.flip-leave-to {
		/* transform: scaleY(0) translateZ(0); */
		transform: rotateY(180deg);
		opacity: 0;
	}
	.fade-enter-active,
	.fade-leave-active {
		transition: all 1s ease-in;
	}
	.fade-enter,
	.fade-leave-to {
		opacity: 0;
	}
</style>