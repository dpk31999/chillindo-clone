<template>
  <div class="main-layout">
    <header />
    <navbar />

    <div class="container mt-4">
      <child />
    </div>
  </div>
</template>

<script>
import Navbar from '~/components/Navbar'
// import Header from '../components/Header.vue'
// import Footer from '../components/Footer.vue'
export default {
  name: 'MainLayout',

  components: {
    Navbar,
    // Header,
    // Footer
  }
}
</script>
