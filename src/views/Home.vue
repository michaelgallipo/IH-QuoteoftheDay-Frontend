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
      <div>
        <input id="numberEntry" type="text" v-model="phone" placeholder="(xxx) xxx-xxxx">
      </div>
      <div id="phoneButtons">
        <button id="save" v-on:click="saveNumber">Subscribe</button>
        <button id="delete" v-on:click="removeNumber">Unsubscribe</button>
      </div>
    </main>

  </div>
</template>

<script>
  const axios = require("axios");
  const qs = require("qs");
  // const FormData = require("form-data");
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

  },
  methods: {
    saveNumber: function() {
      const exist = this.phoneNumbers.filter(num => num.phone === this.phone);
      if (exist.length > 0) {
        if (exist[0].active) {
          window.alert('This number, ' + this.phone + ' is already subscribed');
        }
        else {
          const data = {active: true};
          axios.put("/numbers/" + exist[0]._id, qs.stringify(data))
          .then(response => {
            if (response.status === 200) {
              window.alert('Your number is now subscribed');
            }
          })
        }
      }
      else {
        var phData = {phone: this.phone, active: true};
        axios.post("/numbers", qs.stringify(phData), {
          headers: {
            'Content-Type': 'application/x-www-form-urlencoded'
          }
        })
          .then(response => {
            if (response.status === 200) {
              window.alert('Your number was successfully registered');
              this.phone = "";
            }
          })
          .catch(err => {
            this.error = err
          })
      }
    },
    removeNumber: function() {
      let updateNumber = this.phoneNumbers.filter(num => num.phone === this.phone);
      if (updateNumber.length > 0 && updateNumber[0].active) {
        let data = {active: false}
        axios.put("/numbers/" + updateNumber[0]._id, qs.stringify(data))
          .then(response => {
            if (response.status === 200) {
              window.alert('Your number was successfully unsubscribed')
              this.phone = "";
            }
          })
          .catch(err => {
            this.error = err;
          })
      }
      else {
        window.alert('The number you entered,' + this.phone + ' is not currently subscribed');
      }
    }
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

#numberEntry {
  height: 25px;
  font-size: 16px;
  border-width: 2px;
  margin-top: 10px;
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

#save {
  background-color: navy;
}

#delete {
  background-color: crimson;
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
