<template>
  <div id="app">
    <!-- <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div> -->
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
    <router-view/>
  </div>
</template>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#nav {
  padding: 10px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}

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

button {
  height: 40px;
  width: 100px;
  margin-top: 20px;
  color: white;
  font-weight: bold;
  border-width: 2px;
  margin-left: 10px;
  margin-right: 10px;
}

button:hover {
  cursor: pointer;
}

</style>
