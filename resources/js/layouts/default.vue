<template>
  <div class="main-layout">
    <Header />
    <navbar />

    <div class="container mt-4">
      <child />
    </div>
    <Footer />
  </div>
</template>

<script>
import Navbar from '~/components/Navbar'
import Header from '../components/Header.vue'
import Footer from '../components/Footer.vue'
export default {
  name: 'MainLayout',

  components: {
    Navbar,
    Header,
    Footer
  }
}
</script>
