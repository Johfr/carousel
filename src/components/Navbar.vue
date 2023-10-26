<script setup>
import BurgerMenu from '../components/BurgerMenu.vue'
import CarouselLogo from '../components/CarouselLogo.vue'
</script>

<template>
	<nav>
		<ul class="list">
			<li>About</li>
			<li>News</li>
			<li>Contact</li>
		</ul>

		<p class="logo">
			<CarouselLogo />
			Unseen.
		</p>

		<BurgerMenu class="burgerIcon" />
		<ul class="list">
			<li>Services</li>
			<li>Works</li>
			<li>
				<button>
					Sign up
				</button>
			</li>
		</ul>
	</nav>
</template>

<style lang="scss" scoped>
nav {
	display: flex;
	justify-content: space-between;
	align-items: center;
	min-width: 80%;
	max-width: 80%;
	margin-left: auto;
	margin-right: auto;
	color: #fff;
	position: relative;
	z-index: 3;
	font-family: 'Roboto', sans-serif;
	animation: slideDown 3s 1s forwards;
	opacity: 0;
	.burgerIcon {
		width: 18px;
		height: 18px;
		fill: rgba(255, 255, 255, 0.7);
		
		@media screen and (min-width: 1080px) {
			display: none;
		}
	}
	

	.logo {
		display: flex;
		align-items: flex-start;
		font-size: 1.4rem;
		
		svg {
			width: 25px;
			height: 25px;
			margin-right: 5px;
			fill: #fff;
		}
	}
		
	.list {
		display: none;
		@media screen and (min-width: 1080px) {
			display: flex;
			align-items: center;

			li {
				cursor: pointer;
				transition: .4s ease;

				&:hover {
					opacity: .6;
				}

				&:not(:last-child) {
					margin-right: 30px;
				}
			}
		}
	}
}

.fog {
    width: 100%;
    height: 60vh;
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    z-index: 1;

}

@keyframes slideDown {
	from {
		transform: translateY(-100px);
		opacity: 0;
	}
	to {
		transform: translateY(0);
		opacity: 1;
	}
}
</style>
