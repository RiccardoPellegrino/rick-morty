<template>
  <AppHeader title="Rick and Morty App" />
  <main>
    <AppSearch />
    <CharacterList :characters="characterList" :loading="loading2" />
  </main>
</template>

<script>

import axios from 'axios';
import AppHeader from './components/AppHeader.vue'
import AppSearch from './components/AppSearch.vue'
import CharacterList from './components/CharacterList.vue'

export default {
  components: {
    AppHeader,
    AppSearch,
    CharacterList
  },
  data() {
    return {
      apiURL: 'https://rickandmortyapi.com/api/character',
      characterList: [],
      loading: false
    }
  },
  methods: {
    //chiamata per api come metodo
    getCharacters() {
      this.loading = true;
      axios.get(this.apiURL).then(
        (res) => {
          this.characterList = [...res.data.results]
          console.log(this.characterList)
          this.loading = false;
        },//success

      )
        .catch((error) => {
          // handle error
          console.log(error);
        })
    }
  },
  created() {
    //chiamata api ad inizio app
    this.getCharacters()
  }
}
</script>

<style lang="scss" scoped>

</style>

