<template>
  <div class="app">
    <Header title="The anime quoter" />
    <Quote :quote="quote" />
    <div class="button-container">
      <button @click="getQuote">Generete</button>
    </div>
  </div>

  {{ this.quotes }}
</template>

<script>
import Header from "./components/HeaderComponent.vue";
import Quote from "./components/QuoteComp.vue";

export default {
  name: "App",
  components: {
    Header,
    Quote,
  },
  data() {
    return {
      quote: {
        content: "Content goes here",
        anime: "Jujutsu Kaisen",
        character: "Itadori Midoriya",
      },
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
    //this.getQuote();
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

  button {
    border: none;
    outline: none;
    background-color: var(--primary);

    padding: 16px 32px;
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
