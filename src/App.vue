<template>
  <div id="app">
    <div class="logo">
      <img alt="Vue logo" width="64" src="https://vuejs.org/images/logo.png" />
    </div>
    <AdminGrid :items="Articles" v-on:newList="saveListToStorage" />
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
    getFromStorage() {
      return window.localStorage.getItem('demo_articles');
    },
    saveToStorage() {
      window.localStorage.setItem(
        'demo_articles',
        JSON.stringify(this.Articles)
      );
    },
    saveListToStorage(newList) {
      console.log('saveListToStorage', newList);
      window.localStorage.setItem('demo_articles', JSON.stringify(newList));
    },
  },
  mounted() {
    let getFromStorage = this.getFromStorage();

    if (this.getFromStorage() == null) {
      this.saveToStorage();
    } else {
      let loadArticles = JSON.parse(getFromStorage);
      this.Articles = loadArticles;

      try {
      } catch (e) {
        this.saveToStorage();
        console.error(e);
      }
    }
  },
};
</script>

<style lang="scss">
@import './scss/main.scss';
</style>
