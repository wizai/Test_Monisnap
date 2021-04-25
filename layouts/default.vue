<template>
  <div class="App">
    <Header/>
    <Navbar/>
    <div class="container">
      <nuxt />
    </div>
    <Footer/>
  </div>
</template>

<script>
import Footer from "~/components/footer.vue";
import Header from "~/components/header.vue";
import Navbar from "~/components/navbar.vue";

export default {
  data() {
    return {}
  },
  components: {
    Footer,
    Header,
    Navbar,
  },
}
</script>

<style lang="scss" scoped>

.App{
  min-height: 100vh;
  @include flexbox();
  @include flex-direction(column);
}
.container{
  position: relative;
  z-index: 1;
  padding: 24px 12px;
  background-color: $white;
  @include flex-grow(1);
  ::v-deep section{
    margin-left: auto;
    margin-right: auto;
    max-width: 800px;
  }
}

.page-enter-active,
.page-leave-active {
  @include transition(opacity 0.25s ease-in-out, transform 0.25s ease-in-out);
}
.page-enter,
.page-leave-to {
  opacity: 0;
  @include transform(translate3d(0, 15px, 0));
}




</style>
