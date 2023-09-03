<template>
  <header>
    <h1>
      {{ wordObject.word }}
    </h1>
    <button
      v-if="
        wordObject.phonetics?.filter((object) => object.audio !== '')[0]?.audio
      "
      @click.prevent="
        playSound(
          wordObject.phonetics.filter((object) => object.audio !== '')[0].audio
        )
      "
    >
      <svg
        xmlns="http://www.w3.org/2000/svg"
        viewBox="0 0 24 24"
        fill="currentColor"
        class="w-6 h-6"
      >
        <path
          fill-rule="evenodd"
          d="M4.5 5.653c0-1.426 1.529-2.33 2.779-1.643l11.54 6.348c1.295.712 1.295 2.573 0 3.285L7.28 19.991c-1.25.687-2.779-.217-2.779-1.643V5.653z"
          clip-rule="evenodd"
        />
      </svg>
    </button>
    <p>
      {{
        wordObject.phonetics[1]
          ? wordObject.phonetics[1].text
          : wordObject.phonetics[0].text
      }}
    </p>
  </header>
  <div
    class="part-of-speech"
    v-for="(partOfSpeech, index) in wordObject.meanings"
    :key="index"
  >
    <div class="part-of-speech-header">
      <h2>
        {{ partOfSpeech.partOfSpeech }}
      </h2>
      <hr />
    </div>
    <h3>Meanings</h3>
    <ul>
      <li v-for="(definition, index) in partOfSpeech.definitions" :key="index">
        {{ definition.definition }}
      </li>
    </ul>
    <h3 v-if="partOfSpeech.synonyms[0]">Synonyms</h3>
    <span> {{ partOfSpeech.synonyms.slice(0, 4).join(", ") }}</span>
  </div>
</template>
<script>
export default {
  name: "WordDisplay",
  methods: {
    playSound(sound) {
      if (sound) {
        const audio = new Audio(sound);
        audio.play();
      }
    },
  },
  props: { wordObject: Object },
};
</script>
<style lang="scss" scoped>
header {
  margin-bottom: 2.4rem;
  display: grid;
  grid-template-columns: 1fr auto;

  h1 {
    font-size: 4.8rem;
    line-height: 1.2;
    margin-bottom: 0.8rem;
  }

  p {
    font-size: 2rem;
    color: red;
    grid-column: 1;
  }

  button {
    border: none;
    outline: none;
    background-color: transparentize(red, 0.8);
    height: 6.4rem;
    width: 6.4rem;
    border-radius: 50%;
    color: red;
    padding: 1.6rem;
    grid-column: 2/3;
    grid-row: 1/3;
    align-self: center;
    transition: all 300ms ease-in-out;

    &:hover {
      background-color: transparentize(red, 0.6);
    }
  }
}
.part-of-speech {
  margin-bottom: 3.6rem;

  &-header {
    display: grid;
    grid-template-columns: auto 1fr;
    gap: 2.4rem;
    margin-bottom: 2rem;

    h2 {
      font-size: 2.4rem;
      // margin-bottom: 2.4rem;
    }

    hr {
      border: none;
      height: 1px;
      background-color: lightgrey;
      align-self: center;
    }
  }
  h3 {
    color: grey;
    margin-bottom: 1.8rem;
    font-weight: 500;
  }
  ul {
    margin-bottom: 2.4rem;
    display: flex;
    flex-direction: column;
    gap: 1.2rem;

    li {
      padding-left: 2rem;
      display: block;

      // bullet points
      &::before {
        content: "•";
        color: red;
        font-weight: bold;
        display: inline-block;
        width: 1em;
        margin-left: -1em;
      }
    }
  }
}
</style>
