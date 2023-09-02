<template>
  <h1>
    {{ wordObject.word }}
  </h1>
  <button
    v-if="wordObject.phonetics.filter((object) => object.audio !== '')[0].audio"
    @click.prevent="
      playSound(
        wordObject.phonetics.filter((object) => object.audio !== '')[0].audio
      )
    "
  >
    Play Icon Placeholder
  </button>
  <p>
    {{
      wordObject.phonetics[1]
        ? wordObject.phonetics[1].text
        : wordObject.phonetics[0].text
    }}
  </p>
  <div v-for="(partOfSpeech, index) in wordObject.meanings" :key="index">
    <h2>{{ partOfSpeech.partOfSpeech }}</h2>
    <h3>Meanings:</h3>
    <ul>
      <li v-for="(definition, index) in partOfSpeech.definitions" :key="index">
        {{ definition.definition }}
      </li>
    </ul>
    <h3 v-if="partOfSpeech.synonyms[0]">Synonyms:</h3>
    <span> {{ partOfSpeech.synonyms.slice(0, 4).join(", ") }}</span>
    <hr />
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
<style lang="scss">
ul {
  li {
    padding-left: 2rem;
    display: block;
    &::before {
      content: "\2022";
      color: red;
      font-weight: bold;
      display: inline-block;
      width: 1em;
      margin-left: -1em;
    }
  }
}
</style>
