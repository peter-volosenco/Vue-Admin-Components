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

export default {
  name: 'App',
  components: {
    AdminGrid,
  },
  data: function () {
    return {
      Articles: [
        {
          Id: 'dbfb8245-6f2f-4d31-96f4-f7764ebb3e0b',
          Name: 'Test 1',
          Text: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Cras porta sem finibus eros sodales, a auctor sem rutrum. Fusce pharetra blandit mauris, ac ornare nunc semper vel.',
          Order: 1,
        },
        {
          Id: '898a4bbc-74d9-4a2d-8b54-6b1660379320',
          Name: 'Test 2',
          Text: 'Nam tincidunt sollicitudin nulla, sit amet suscipit ante malesuada in. Nulla sit amet nisi vel massa lacinia dictum sit amet id velit. Integer vel massa eros. ',
          Order: 2,
        },
        {
          Id: '898a4bbc-74d9-4a2d-8b54-6b1660379321',
          Name: 'Test 3',
          Text: 'Nam tincidunt sollicitudin nulla, sit amet suscipit ante malesuada in. Nulla sit amet nisi vel massa lacinia dictum sit amet id velit. Integer vel massa eros. ',
          Order: 3,
        },
        {
          Id: '898a4bbc-74d9-4a2d-8b54-6b1660379322',
          Name: 'Test 4',
          Text: 'Nam tincidunt sollicitudin nulla, sit amet suscipit ante malesuada in. Nulla sit amet nisi vel massa lacinia dictum sit amet id velit. Integer vel massa eros. ',
          Order: 4,
        },
      ],
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
