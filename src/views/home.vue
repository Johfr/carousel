<script setup>
import { ref } from 'vue'
import Navbar from '../components/Navbar.vue'
import Carousel from '../components/CarouselComponent.vue'

const homeBgColor = ['#3a4e65', '#5c6d77', '#9299be', '#312415', '#30495a', '#8dc3e5']
const bg = ref(homeBgColor[0])

const changeBgColor = (index) => {
	if (index > homeBgColor.length -1) {
		const randomColor = Math.round(Math.random() * 10)
		
		// applique une couleur prédéfinie ou du noir
		if (randomColor <= homeBgColor.length) {
			bg.value = homeBgColor[randomColor]
		} else {
			bg.value = '#000'
		}
	} else {
		bg.value = homeBgColor[index]
	}
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
</style>
