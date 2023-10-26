<script setup>
import { ref, defineEmits, defineProps } from 'vue'
import Arrow from '../components/Arrow.vue'

const props = defineProps({
	nearImg: {
		type: Boolean,
		default: false
	},
	data: {
		type: Array,
		default: [
			{
				title: "Himalaya under fog",
				desc: "Himalaya with fog - Project by Peter Magnus",
				img: "src/assets/img/himalaya.jpg"
			},
			{
				title: "Lighthouse",
				desc: "Lighthouse Under water - Project by John Peterson",
				img: "src/assets/img/lighthouse.jpg"
			},
		]
	}
})

const emit = defineEmits(['bgColor'])

let slideToDisplay = ref(0)
let isPrev = ref(false)

const showPrev = () => {
	slideToDisplay.value -= 1
	isPrev.value = true

	if (slideToDisplay.value < 0) {
		slideToDisplay.value = props.data.length - 1
	}
	
	emit('bgColor', slideToDisplay.value)
}

const showNext = () => {
	slideToDisplay.value += 1
	isPrev.value = false

	if (slideToDisplay.value > props.data.length - 1) {
		slideToDisplay.value = 0
	}
	
	emit('bgColor', slideToDisplay.value)
}

const goFirstOrLast = () => {
	slideToDisplay.value === props.data.length -1 ? slideToDisplay.value = 0 : slideToDisplay.value = props.data.length -1
	emit('bgColor', slideToDisplay.value)
	return slideToDisplay.value
}
</script>

<template>
	<section>
		<button class="arrow-container prev" @click="showPrev" :disabled="slideToDisplay === 0 ? true : false" title="Previous">
			<Arrow class="arrow-left arrow-icon" />
			<p>Previous</p>
		</button>

		<ul class="list">
			<li
				class="item"
				v-for="(item, itemId) in data" :key="itemId"
				:class="{ancestor: itemId < slideToDisplay - 1, previous: itemId < slideToDisplay, active: itemId === slideToDisplay, next: itemId > slideToDisplay, grandChild: itemId > slideToDisplay + 1, 'close-img':  nearImg }"
				@click="slideToDisplay = itemId"
				:title="item.title"
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
		
		<button class="arrow-container next" @click="showNext" :disabled="slideToDisplay === data.length - 1 ? true : false" title="Next">
			<Arrow class="arrow-left arrow-icon" />
			<p>Next</p>
		</button>

		<button @click="goFirstOrLast" class="quick-end-button" :title='slideToDisplay === data.length -1 ? "Go to First slide" : "Go to last end"'>
			<span>
				{{ slideToDisplay === data.length -1 ? "First slide" : "Quick end" }}
			</span>
		</button>
	</section>
</template>

<style lang="scss" scoped>
section {
	width: 100%;
	display: flex;
	justify-content: center;
	align-items: center;
	position: relative;

	.arrow-container {
		width: 55px;
		height: 55px;
		display: flex;
		justify-content: center;
		align-items: center;
		background-color: rgba(0, 0, 0, .5);
		position: absolute;
		bottom: 30px;
		border-radius: 50%;
		z-index: 3;
		cursor: pointer;

		@media screen and (min-width: 900px) {
			width: 100px;
			height: 100px;
			top: 50%;
			bottom: unset;
		}

		&.prev {
			left: 10px;
			@media screen and (min-width: 900px) {
				left: 10%;
			}
		}

		&.next {
			right: 10px;
			.arrow-icon {
				transform: rotate(180deg);
			}
			@media screen and (min-width: 900px) {
				right: 10%;
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
			display: none;
			@media screen and (min-width: 900px) {
				position: absolute;
				bottom: -130%;
			}
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
		cursor: pointer;

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
			width: 285px;
			height: 285px;
			
			.img-container {
				width: 285px;
				height: 285px;
			}
			img {
				width: 100%;
				height: 100%;
    		filter: opacity(.5);
			}

			.content {
				animation: slideDown .6s forwards;
			}
		}
		&.previous {
			right: 80%;
			&.ancestor {
				width: 50px;
				height: 50px;
				overflow: hidden;
				right: 100%;
				left: unset;
				transform: translate(0%, -50%);
			}

			@media screen and (min-width: 900px) {
				transform: translate(0%, -50%) rotate(-180deg);
				&.close-img {
					right: 60%;
					&.ancestor {
						right: 80%;
					}
				}
			}
		}
		&.next {
			right: 5%;
			left: unset;
			
			&.grandChild {
				width: 50px;
				height: 50px;
				overflow: hidden;
				right: -33%;
				left: unset;
				transform: translate(0%, -50%);
				z-index: -1;
			}

			@media screen and (min-width: 900px) {
				transform: translate(0%, -50%) rotate(180deg);
				&.close-img {
					right: 25%;
					&.grandChild {
						right: 21%;
					}
				}
			}
		}

		&.active {
    	width: 320px;
			height: 500px;
			right: 50%;
    		transform: translate(50%, -50%);
			z-index: 2;
			overflow: visible;
			
			@media screen and (min-width: 900px) {
				width: 485px;
				height: 750px;
			}
			
			.img-container {
				width: 100%;
				width: 320px;
				height: 500px;
				@media screen and (min-width: 900px) {
					width: 485px;
					height: 750px;
				}
			}
			img {
				width: 100%;
				width: 320px;
				height: 500px;
				@media screen and (min-width: 900px) {
					width: 485px;
					height: 750px;
				}
			}

			.content {
    			padding: 16px;
				overflow: visible;
				background-color: rgba(0, 0, 0, .2);
				
				@media screen and (min-width: 900px) {
					background-color: rgba(255, 255, 255, .3);
				}

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
			top: 0;
			left: 0;
			right: 0;
			overflow: hidden;
			
			@media screen and (min-width: 900px) {
				top: 50%;
				left: -23px;
				right: unset;
			}

			h1 {
				margin-top: 0;
				margin-bottom: 0;
				font-size: 2.2rem;
				padding-left: 30px;
				font-weight: 500;
				@media screen and (min-width: 900px) {
					padding-left: unset;
					font-size: 3.2rem;
				}
			}
		}
	}
}

.quick-end-button {
	padding: 15px 35px;
	background-color: #1d2732b3;
	position: absolute;
	bottom: 50px;
	left: 50%;
	transform: translateX(-50%);
	box-shadow: 0px 2px 2px #1d2732;
	border: unset;
	z-index: 3;

	&:hover {
		border: unset;
		box-shadow: unset;
	}

	&:focus,
	&:focus-visible {
		outline: unset;
		border: unset;
		box-shadow: unset;
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
