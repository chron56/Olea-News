<template>
  <div id="app">
    <Header />
    <Articles />
    <Footer />
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Articles from './components/Articles.vue'
import Footer from './components/Footer.vue'

export default {
  name: 'app',
  components: {
    Header,
    Articles,
    Footer
  }
}
</script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
  }
</style>