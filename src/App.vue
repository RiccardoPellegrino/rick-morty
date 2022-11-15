<template>
  <AppHeader title="Rick and Morty App" />
  <main>
    <AppSearch @filterChar="getCharacters" />
    <CharacterList />
    <div v-if="store.errorMessage">
      <h1 class="text-center mt-5">opps ! Qualcosa è andato storto</h1>
      <p class="text-center">{{ store.errorMessage }}</p>
    </div>
    <ResultCount />
  </main>
</template>

<script>

import axios from 'axios';
import AppHeader from './components/AppHeader.vue'
import AppSearch from './components/AppSearch.vue'
import CharacterList from './components/CharacterList.vue'
import ResultCount from './components/ResultCount.vue';
import { store } from './store';


export default {
  components: {
    AppHeader,
    AppSearch,
    CharacterList,
    ResultCount
  },
  data() {
    return {
      store,
      endPoint: 'character',
    }
  },
  watch: {

  },
  methods: {
    //chiamata per api come metodo
    getCharacters() {
      store.errorMessage = '';
      // const nuovoApiUrl = (status) ? this.apiURL + '?status=' + status : this.apiURL;
      let options = null

      if (store.searchStatus && store.searchName) {
        options = {
          params: {
            status: store.searchStatus,
            name: store.searchName
          }
        }
      } else if (store.searchStatus) {
        options = {
          params: {
            status: store.searchStatus,
          }
        }
      }
      else if (store.searchName) {
        options = {
          params: {
            name: store.searchName,
          }
        }
      }

      store.loading = true;
      // if (status) {
      //   const nuovoApiUrl = this.apiURL + '?status=' + status;
      // }
      const apiurl = store.apiURL + this.endPoint;
      axios.get(apiurl, options).then(
        (res) => {
          store.characterList = [...res.data.results]
          store.loading = false;
        },//success

      )
        .catch((error) => {
          // handle error
          store.characterList.length = 0;
          store.loading = false;
          store.errorMessage = error.message
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

