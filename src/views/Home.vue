<template>
  <div class="home">
    <header>
			<img
				class="headerImage"
				id="leftImage"
				alt="Hippo logo"
				src="./assets/images/hippo.jpg"
			/>
			<p class="title">Internet Hippo's Quote of the Day</p>
			<img
				class="headerImage"
				id="rightImage"
				alt="Hippo logo"
				src="./assets/images/hippo.jpg"
			/>
		</header>

  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'home',
  // components: {
  //   HelloWorld
  // }
}
</script>

<style scoped>

.headerImage {
	width: 150px;
	height: 150px;
	position: absolute;
	padding: 20px;
}
#leftImage {
	top: 0px;
	left: 0px;
}
#rightImage {
	top: 0px;
	right: 0px;
}

.title {
	font-size: 46px;
	font-weight: bold;
	text-align: center;
	font-family: cursive;
}

@media screen and (max-width: 950px) {
	.headerImage {
		position: relative;
	}
	#rightImage {
		display: none;
	}
}
</style>
