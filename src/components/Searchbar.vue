<template>
  <form @submit.prevent="formSubmitted()">
    <input
      v-model="searchedValue"
      type="text"
      name="searchBarInput"
      id="searchBarInput"
      placeholder="Enter a word you want to look for"
    />
    <button type="submit">
      <svg
        xmlns="http://www.w3.org/2000/svg"
        fill="none"
        viewBox="0 0 24 24"
        stroke-width="2"
        stroke="currentColor"
        class="w-6 h-6"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          d="M21 21l-5.197-5.197m0 0A7.5 7.5 0 105.196 5.196a7.5 7.5 0 0010.607 10.607z"
        />
      </svg>
    </button>
  </form>
</template>

<script>
export default {
  name: "Searchbar",
  data() {
    return {
      searchedValue: "",
    };
  },
  methods: {
    formSubmitted() {
      console.log(this.searchedValue);
      this.$emit("searchingForWord", this.searchedValue);
    },
  },
  emits: ["searchingForWord"],
};
</script>
<style lang="scss" scoped>
@import "../assets/styles/abstracts.scss";
form {
  background-color: lightgrey;

  display: grid;
  grid-template-columns: 1fr auto;
  padding: 0.8rem 1.2rem 0.8rem 1.8rem;
  border-radius: 1rem;

  input {
    font-size: 2rem;

    background-color: transparent;

    outline: none;
    border: none;
    width: 90%;
  }

  button {
    background-color: transparent;

    border: none;
    width: 3rem;
  }
}
</style>
