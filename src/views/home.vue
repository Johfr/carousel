<script setup>
import { ref } from 'vue'
import Navbar from '../components/Navbar.vue'
import Carousel from '../components/CarouselComponent.vue'

const data = [
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
	{
		title: "Montgolfière",
		desc: "hot air balloon - Project by James K",
		img: "src/assets/img/air-balloon.jpg"
	},
	{
		title: "Natural lake",
		desc: "Nature - Project by Keanu R",
		img: "src/assets/img/natural-lake.jpg"
	},
	{
		title: "Feel lonely",
		desc: "Park - Project by Akon X",
		img: "src/assets/img/lonely.jpg"
	},
	{
		title: "Blue Sea",
		desc: "Public park seat - Project by Mary X",
		img: "src/assets/img/monument.jpg"
	},
]

const homeBgColor = ['#3a4e65', '#5c6d77', '#9299be', '#312415', '#30495a', '#8dc3e5', '#7b4343']
const bg = ref(homeBgColor[0])

const changeBgColor = (index) => {
	if (index > homeBgColor.length -1) {
		const randomColor = Math.round(Math.random() * 10)
		
		// applique une couleur prédéfinie ou du noir
		if (randomColor <= homeBgColor.length - 1) {
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
		<Carousel @bgColor="changeBgColor" :data="data"/>
		<Carousel @bgColor="changeBgColor" :nearImg="true" :data="data"/>
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
