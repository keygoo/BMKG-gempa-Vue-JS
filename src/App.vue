<template>
  <v-app>
    <v-main>
      <Header/>
      <Gempa/>
      <Footer/>
    </v-main>
  </v-app>
</template>

<script>
import Header from './components/template-part/header.vue'
import Gempa from './components/Gempa.vue'
import Footer from './components/template-part/footer.vue'

export default {
  name: 'App',

  components: {
    Header,
    Gempa,
    Footer
  },

};
</script>
