<script setup>
import { ref } from 'vue'
import Navbar from '../components/Navbar.vue'
import Carousel from '../components/CarouselComponent.vue'

const homeBgColor = ['#8dc3e5', '#5c6d77', '#9299be', '#8dc3e5',]
const bg = ref(homeBgColor[1])

const changeBgColor = (index) => {
	bg.value = homeBgColor[index]
}

</script>

<template>
	<div class="home">
		<Navbar />
		<Carousel @bgColor="changeBgColor" />
	</div>
</template>

<style lang="scss" scoped>
.home {
	min-height: 100vh;
	max-height: 100vh;
	overflow-x: hidden;
	position: relative;
  background-color: v-bind(bg);
	transition: .6s ease-out;
}
// @keyframes slideUp {
// 	0% {
// 		transform: translateY(200px);
// 		opacity: 0;
// 	}
// 	70% {
// 		opacity: 0.3;
// 	}
// 	100% {
// 		transform: translateY(0);
// 		opacity: 1;
// 	}
// }
</style>
