<template>
  <footer>
    <div class="footer">
      <img class="footer__logo" src="~/assets/img/logo_white.svg" />
      <p class="footer__text">Made with <span>&#10084;</span> in Paris</p>
    </div>
  </footer>
</template>

<script>
export default {
  name: "Footer"
}
</script>

<style lang="scss" scoped>

.footer{
  height: 108px;
  background-color: $blue;
  position: relative;
  margin-top: auto;
  @include flexbox();
  @include align-items(center);
  @include justify-content(center);
  @include flex-flow(column wrap);
  &__text{
    position: absolute;
    left: 0;
    right: 0;
    bottom: 15px;
    font-size: 8px;
    color: $white;
    text-align: center;
    span{
      color: red;
    }
  }
}

</style>
