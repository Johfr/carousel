<script setup>
import { ref, defineEmits } from 'vue'
import Arrow from '../components/Arrow.vue'

const emit = defineEmits(['bgColor'])

const data = [
	{
		title: "Blue Sea",
		desc: "Under Water Creature - Project by Mary X",
		img: "src/assets/img/monument.jpg"
	},
	{
		title: "Blue Sea",
		desc: "Up-Above Water Monumment - Project by Mary X",
		img: "src/assets/img/lighthouse.jpg"
	},
	{
		title: "Blue Sea",
		desc: "Under Water Creature - Project by Mary X",
		img: "src/assets/img/air-balloon.jpg"
	},
	{
		title: "Blue Sea",
		desc: "Up-Above Water Monumment - Project by Mary X",
		img: "src/assets/img/monument.jpg"
	},
]

let firstDataToDisplay = ref(1)
let isPrev = ref(false)

const showPrev = () => {
	firstDataToDisplay.value -= 1
	isPrev.value = true

	if (firstDataToDisplay.value < 0) {
		firstDataToDisplay.value = data.length - 1
	}
	
	emit('bgColor', firstDataToDisplay.value)
}

const showNext = () => {
	firstDataToDisplay.value += 1
	isPrev.value = false

	if (firstDataToDisplay.value > data.length - 1) {
		firstDataToDisplay.value = 0
	}
	
	emit('bgColor', firstDataToDisplay.value)
}

</script>

<template>
	<section>
		<button class="arrow-container prev" @click="showPrev" :disabled="firstDataToDisplay === 0 ? true : false">
			<Arrow class="arrow-left arrow-icon" />
			<p>Previous</p>
		</button>
		<!-- v-show="itemId === firstDataToDisplay || itemId === firstDataToDisplay - 1 || itemId === firstDataToDisplay + 1" -->
		<ul class="list">
			<li
				class="item"
				v-for="(item, itemId) in data" :key="itemId"
				:class="{ancestor: itemId < firstDataToDisplay - 1, previous: itemId < firstDataToDisplay, active: itemId === firstDataToDisplay, next: itemId > firstDataToDisplay, grandChild: itemId > firstDataToDisplay + 1 }"
			>
				<div class="img-container">
					<img :src="item.img" alt="">
				</div>

				<div class="content">
					<h1>
						{{ item.title }}
					</h1>
					<p>
						{{ item.desc }}
					</p>
				</div>
			</li>
		</ul>
		
		<button class="arrow-container next" @click="showNext" :disabled="firstDataToDisplay === data.length - 1 ? true : false">
			<Arrow class="arrow-left arrow-icon" />
			<p>Next</p>
		</button>
	</section>
</template>

<style lang="scss" scoped>
section {
	width: 100%;
	display: flex;
	justify-content: center;
	align-items: center;
	// position: relative;

	.arrow-container {
		width: 100px;
		height: 100px;
		display: flex;
		justify-content: center;
		align-items: center;
		background-color: rgba(0, 0, 0, .5);
		position: absolute;
		top: 50%;
		border-radius: 50%;
		z-index: 3;
		cursor: pointer;

		&.prev {
			left: 10%;
		}

		&.next {
			right: 10%;
			.arrow-icon {
				transform: rotate(180deg);
			}
		}

		.arrow-icon {
			width: 50px;
			height: 50px;
			fill: #fff;
		}

		&:disabled {
			cursor: not-allowed;
			opacity: .4;
		}

		p {
			position: absolute;
			bottom: -130%;
		}
	}
	.list {
		display: flex;
		justify-content: center;
    width: 100%;
		height: calc(100vh - 72px);
    margin: 0 auto;
    overflow: hidden;
		position: relative;
		opacity: 0;
		animation: fade 4s .4s forwards;
	}

	.item {
		display: flex;
		justify-content: center;
		align-items: center;
		width: 285px;
		height: 285px;
		overflow: hidden;
		position: absolute;
		top: 50%;
		transform: translateY(-50%);
		transition: 1s ease;

		.img-container {
			width: 285px;
			height: 500px;
			overflow: hidden;
			transition: 1s ease;
			
			img {
				width: 285px;
				height: 500px;
				object-fit: cover;
			}
		}

		&.previous, &.next {
			.img-container {
				width: 285px;
				height: 500px;
			}
			img {
				width: 100%;
				height: 100%;
			}

			.content {
				animation: slideDown .6s forwards;
			}
		}
		&.previous {
			right: 80%;
			// left: 5%; // affect la fluidité de l'animation - bon pour le responsive (+) // rajouter une class en timeout ?
    	transform: translate(0%, -50%) rotate(-180deg);
			&.ancestor {
				width: 50px;
				height: 50px;
				overflow: hidden;
				right: 100%;
				left: unset;
				transform: translate(0%, -50%);
			}
		}
		&.next {
			right: 5%;
			left: unset;
    	transform: translate(0%, -50%) rotate(180deg);
			
			&.grandChild {
				width: 50px;
				height: 50px;
				overflow: hidden;
				right: -33%;
				left: unset;
				transform: translate(0%, -50%);
			}
		}

		&.active {
			width: 485px;
			height: 800px;
			right: 50%;
    	transform: translate(50%, -50%);
			z-index: 2;
			overflow: visible;
			
			.img-container {
				width: 485px;
				height: 800px;
			}
			img {
				width: 485px;
				height: 800px;
			}

			.content {
    		padding: 16px;
				background-color: rgba(255, 255, 255, .3);
				overflow: visible;
				h1 {
					animation: slideUp 2s forwards;
				}
				p {
					opacity: 0;
					animation: slideUp 2s .4s forwards;
					padding-left: 30px;
				}
			}
		}

		.content {
			position: absolute;
			top: 50%;
			left: -23px;
			overflow: hidden;

			h1 {
				margin-top: 0;
				margin-bottom: 0;
				font-weight: 500;
			}
		}
	}
}

@keyframes rotate {
	0% {
		transform: translate(50%, -50%) rotate(180deg);
	}
	100% {
		transform: translate(50%, -50%) rotate(0);
	}
}

@keyframes fade {
	0% {
		opacity: 0;
	}
	100% {
		opacity: 1;
	}
}

@keyframes slideUp {
	0% {
		opacity: 0;
		transform: translate(-30px, 100px) skewY(10deg);
	}
	100% {
		opacity: 1;
		transform: translate(-30px, 0) skewY(0deg);
	}
}

@keyframes slideDown {
	0% {
		opacity: 1;
		transform: translate(-30px, 0) skewY(0deg);
	}
	100% {
		opacity: 0;
		transform: translate(-30px, 100px) skewY(10deg);
	}
}
</style>
