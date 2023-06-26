<script setup>
import BurgerMenu from '../components/BurgerMenu.vue'
</script>

<template>
	<nav>
		<p class="logo">Unseen</p>

		<BurgerMenu class="burgerIcon" />
		<ul class="list">
			<li>About</li>
			<li>Blog</li>
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
	text-transform: uppercase;
	animation: slideDown 3s 1s forwards;
	opacity: 0;
	.burgerIcon {
		width: 18px;
		height: 18px;
		path {
			fill: rgba(0, 0, 0, 0.7)
		}
		@media screen and (min-width: 1080px) {
			display: none;
		}
	}
	

	.logo {
		letter-spacing: 5px;
	}


		
	.list {
		display: none;
		@media screen and (min-width: 1080px) {
			display: flex;
			align-items: center;

			li {
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
