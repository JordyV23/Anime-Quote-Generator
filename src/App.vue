<template>
  <div class="app">
    <Header title="Frasanime" />
    <Quote :quote="quote" />
    <div class="button-container">
      <button @click="getQuote" class="button">Generar</button>
      <button @click="translate" class="button">Traducir</button>
    </div>
  </div>

  <QuoteList :quotes="quotes" />

  <Footer />
</template>

<script>
import Header from "./components/HeaderComponent.vue";
import Quote from "./components/QuoteComp.vue";
import QuoteList from "./components/QuoteList.vue";
import Footer from "./components/MyFooter.vue";

export default {
  name: "App",
  components: {
    Header,
    Quote,
    QuoteList,
    Footer,
  },
  data() {
    return {
      quote: {
        content: "",
        anime: "",
        character: "",
      },
      quotes: [],
      idiom: "en|es",
    };
  },
  methods: {
    async getQuote() {
      this.idiom = "en|es";
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

    async translate() {
      const data = await fetch(
        `https://api.mymemory.translated.net/get?q=${this.quote.content}&langpair=${this.idiom}`
      ).then((res) => res.json());
      this.quote = {
        content: data.responseData.translatedText,
        anime: this.quote.anime,
        character: this.quote.character,
      };
      this.idiom = this.idiom == "es|en" ?  "en|es" :  "es|en";
    },
  },

  created() {
    this.getQuote();
  },
};
</script>

<style lang="scss">
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
  font-family: "Fira Sans", sans-serif;
}

.button-container {
  display: flex;
  justify-content: center;
  padding: 0px;
  margin: 64px auto;

  .button {
    border: none;
    outline: none;
    background-color: var(--primary);

    padding: 16px 32px;
    margin: 8px;
    border-radius: 99px;
    color: var(--light);
    font-size: 28px;
    font-weight: 700;
    text-transform: uppercase;
    cursor: pointer;
    transition: 0.4s;

    &:hover {
      background-color: var(--secondary);
    }
  }
}
</style>
