<template>
  <div id="app">
    <div class="logo">
      <img alt="Vue logo" width="64" src="https://vuejs.org/images/logo.png" />
    </div>
    <AdminGrid :items="Articles" v-on:newList="StorageSaveUpdated" />
  </div>
</template>

<script>
import AdminGrid from './components/AdminGrid.vue';
import ArticlesContent from './data/ArticlesContent.js';

export default {
  name: 'App',
  components: {
    AdminGrid,
  },
  data: function () {
    return {
      Articles: ArticlesContent,
    };
  },
  methods: {
    StorageGetLatest() {
      return window.localStorage.getItem('demo_articles');
    },
    StorageInitCopy() {
      window.localStorage.setItem(
        'demo_articles',
        JSON.stringify(this.Articles)
      );
    },
    StorageSaveUpdated(newList) {
      console.log('StorageSaveUpdated', newList);
      window.localStorage.setItem('demo_articles', JSON.stringify(newList));
    },
  },
  mounted() {
    let StorageGetLatest = this.StorageGetLatest();

    if (this.StorageGetLatest() == null) {
      this.StorageInitCopy();
    } else {
      let loadArticles = JSON.parse(StorageGetLatest);
      this.Articles = loadArticles;

      try {
      } catch (e) {
        this.StorageInitCopy();
        console.error(e);
      }
    }
  },
};
</script>

<style lang="scss">
@import './scss/main.scss';
</style>
