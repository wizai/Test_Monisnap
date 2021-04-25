<template>
  <div class="container">
    <div class="container_404">
      <h1 v-if="error.statusCode === 404">404</h1>
      <h1 v-else>Error</h1>
      <h2 v-if="error.statusCode === 404">Oops! Cette page n'est pas disponible</h2>
      <h2 v-else>Une erreur s'est produite</h2>
      <p>Apparemment, rien n'a été trouvé à cette adresse.</p>
      <nuxt-link to="/">Retour au site</nuxt-link>
    </div>

  </div>
</template>

<script>
export default {
  props: ['error'],
  layout: 'errorlayout',
}
</script>

<style lang="scss" scoped>

.container_404{
  text-align: center;
  height: 100vh;
  font-weight: 300;
  width: 100%;
  z-index: 99;
  font-size: 15px;
  padding: 0 20px;
  background-color: #ffffff;
  @include flexbox();
  @include justify-content(center);
  @include flex-flow(column wrap);
  @include box-sizing(border-box);
}
h1{
  font-size: 144px;
  font-weight: 900;
  color: $blue;
  @media #{$desktop} {
    font-size: 15vw;
  }
}
h2{
  font-size: 30px;
  font-weight: 500;
  margin-bottom: 16px;
}
a{
  max-width: 160px;
  margin: 50px auto 0;
  display: inline-block;
  border-radius: 10px;
  padding: 10px 20px;
  color: #ffffff;
  background-color: $blue;
  text-decoration: none;
  border: 2px solid $blue;
  font-weight: 700;
  @include transition(all 0.5s ease-in-out);
  &:hover{
    background-color: #ffffff;
    color: $blue;
  }
}
</style>
