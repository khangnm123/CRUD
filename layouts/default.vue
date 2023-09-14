<template>
  <div class="wallpaper">
    <Header/>
        <Nuxt />
        
    <Footer/>
  </div>
  
</template>

<script>
import Header from '../components/header/Header'
import Footer from '../components/header/Footer'


export default {
  components: {
    Header , Footer
  }
}
</script>
