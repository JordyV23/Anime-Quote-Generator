<template>
  <div class="app">
    <Header title="The anime quoter"/>
    <Quote />
  </div>
</template>

<script>
import Header from './components/HeaderComponent.vue';
import Quote from './components/QuoteComp.vue'

export default {
  name: "App",
  components: {
    Header,
    Quote
  },
};
</script>

<style lang="scss">
:root{
    --primary: #D81E5B;
    --secondary: #8A4FFF;
    --tertiary:#32CBFF;
    --dark: #131A26;
    --light: #EEE;
    --grey: #848484;
}

 *{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Fira Sans', sans-serif;
 }
</style>
