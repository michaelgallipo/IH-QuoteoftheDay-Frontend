<template>
  <div class="home">
    <header>
			<img
				class="headerImage"
				id="leftImage"
				alt="Hippo logo"
				src="../assets/images/hippo.jpg"
			/>
			<p class="title">Internet Hippo's Quote of the Day</p>
			<img
				class="headerImage"
				id="rightImage"
				alt="Hippo logo"
				src="../assets/images/hippo.jpg"
			/>
		</header>
    <main>
      <div id="currentQuote">
        <p>{{currentQuote[0].Quote}}</p>
        <p v-if="currentQuote[0].Source">
          <span>{{currentQuote[0].Author}}</span>
          <span id="quoteSource" v-if="currentQuote[0].Source">, {{currentQuote[0].Source}} </span>
        </p>
      </div>
      <div id="info">
        <p>If you would like to receive the Quote of the Day via Text Message, please enter your phone number below.<br />
        You can unsubscribe at any time by re-entering your phone number and hitting the unsubscribe button.<br />
        Quotes will not repeat in a given calendar year. Database will reset at the start of a new year.
        </p>
      </div>
    </main>

  </div>
</template>

<script>
  const axios = require("axios");
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'home',
  // components: {
  //   HelloWorld
  // }
  data: function() {
    return {
      quotes: [],
      currentQuote: [{Quote: "", Author: "", Source: ""}],
      phone: "",
      phoneNumbers: [],
      error: ""
    };
  },
  created: async function() {
    await axios.get("/quotes").then(response => {
      this.quotes = response.data;
      this.currentQuote = this.quotes.filter(entry => entry.Active == true)
    })
    await axios.get("numbers").then(response => {
      this.phoneNumbers = response.data
      console.log(this.phoneNumbers)
    })

  }
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

#quoteSource {
  font-style: italic
}

#currentQuote {
  padding-top: 15px;
  font-size: 20px;
  color: #000;
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
