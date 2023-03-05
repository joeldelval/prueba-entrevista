<template>
  <v-app>
    <v-main>
      <TopBar @search="fSearch"></TopBar>
      <Catalog :pData="dPost" :pSearch="dSearch"></Catalog>
      <Footer></Footer>
    </v-main>
  </v-app>
</template>

<script>
import Catalog from './components/Catalog.vue';
import Footer from './components/Footer.vue';
import TopBar from './components/TopBar';
import axios from 'axios';

export default {
  name: 'App',
  components: {
    TopBar,
    Catalog,
    Footer
  },
  data: () => ({
    dSearch: '',
    dPost: []
  }),
  mounted () {
    this.fGetData()
  },
  methods: {
    fGetData () {
      axios.get('https://jsonplaceholder.typicode.com/posts').then(response => {
        this.dPost = response.data;
      })
      .catch(error => {
        console.log(error);
      })
      
    },
    fSearch (text) {
      this.dSearch = text
    }
  }
};
</script>
