<template>
  <div class="about">
    <h1>Admin Functions</h1>
    <button id="newQuote" v-on:click="newQuote">Send Quote</button>
  </div>
</template>

<script>
const axios = require("axios");
const qs = require("qs");

export default {
  name: 'about',
  // components: {
  //   HelloWorld
  // }
  data: function() {
    return {
      quotes: [],
      activeQuote: "",
      phoneNumbers: [],
      error: ""
    };
  },
  created: async function() {
    await axios.get("/quotes").then(response => {
      this.quotes = response.data;
      this.activeQuote = this.quotes.filter(entry => entry.Active == true)
    })
    await axios.get("numbers").then(response => {
      this.phoneNumbers = response.data
    })
  },
  methods: {
    newQuote: async function() {
      const unusedQuotes = this.quotes.filter(elem => elem.Active == false && elem.Used == false);
      let random = Math.floor(Math.random() * unusedQuotes.length);
      const newQuote = unusedQuotes[random];
      console.log(newQuote);
      const chgStatus = {Used: true, Active: false};
      await axios.put("/quotes/" + this.activeQuote[0]._id, qs.stringify(chgStatus))
        .then(response => {
          if (response.status >= 200 && response.status <= 210) {
            chgStatus = {Active: true};
            console.log(chgStatus);
          }
        })
        .catch(err => {
          this.error = err;
        })
      await axios.put("/quotes/" + newQuote._id, qs.stringify({Active: true}))
        .then(response => {
          if (response.status === 200) {
              window.alert('Quote Updated');
          }
        })
    }
  }
}
</script>
