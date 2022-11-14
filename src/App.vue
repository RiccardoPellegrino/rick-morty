<template>
  <AppHeader />
  <main>
    <AppSearch />
    <CharacterList />
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
  }
}
</script>

<style lang="scss" scoped>

</style>
