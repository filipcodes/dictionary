<script setup>
import Header from "./components/Header.vue";
import Searchbar from "./components/Searchbar.vue";
import WordDisplay from "./components/WordDisplay.vue";
Header;
</script>

<template>
  <main>
    <Header></Header>
    <div class="container">
      <Searchbar @searchingForWord="searchForWord"></Searchbar>
      <WordDisplay v-if="currentWord" :wordObject="currentWord"></WordDisplay>
    </div>
  </main>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      currentWord: undefined,
    };
  },
  methods: {
    //TODO add an error handler
    async searchForWord(word) {
      try {
        const res = await axios.get(
          `https://api.dictionaryapi.dev/api/v2/entries/en/${word}`
        );
        this.currentWord = await res.data[0];
        console.log(this.currentWord);
      } catch (e) {
        this.currentWord = null;
        // console.log(await res);
      }
    },
  },
};
</script>

<style lang="scss">
@import "./assets/styles/reset.scss";

body {
  font-family: "Roboto Slab", sans-serif;
  font-size: 1.6rem;
}

main {
  max-width: 100rem;
  margin: 0 auto;
}

.container {
  margin: 0 2.4rem;
}
</style>
