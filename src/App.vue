<template>
  <div class="app">
    <Header title="The Anime Quoter" />
    <Quote :quote="quote" />
    <div class="btn-container">
      <button @click="getQuote">Generate</button>
    </div>
    <QuoteList :quotes="quotes" />
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Quote from "./components/Quote.vue";
import QuoteList from "./components/QuoteList.vue";

export default {
  name: "App",
  components: {
    Header,
    Quote,
    QuoteList,
  },
  data() {
    return {
      quote: {},
      quotes: [],
    };
  },
  methods: {
    async getQuote() {
      if (this.quote.content) {
        this.quotes = [...this.quotes, this.quote];
      }

      const data = await fetch("https://animechan.vercel.app/api/random").then(
        (res) => res.json()
      );

      this.quote = {
        content: data.quote,
        anime: data.anime,
        character: data.character,
      };
    },
  },
  created() {
    this.getQuote();
  },
};
</script>

<style Lang="scss">
:root {
  --primary: #d81e5b;
  --secondary: #8a4fff;
  --tertiary: #32cbff;
  --dark: #131a26;
  --light: #eee;
  --grey: #848484;
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  /*font-family: "Fira Sans", sans-serif;*/
  font-family: Cambria, Cochin, Georgia, Times, "Times New Roman", serif;
}
.btn-container {
  display: flex;
  justify-content: center;
  padding: 0px 32px;
  margin: 64px auto;
}

.btn-container > button {
  border: none;
  outline: none;
  color: var(--light);
  background-color: var(--primary);

  padding: 16px 32px;
  border-radius: 99px;
  font-size: 28px;
  font-weight: 700;
  text-transform: uppercase;
  cursor: pointer;
  transition: 0.4s;
}

.btn-container > button:hover {
  background-color: var(--secondary);
}
</style>
