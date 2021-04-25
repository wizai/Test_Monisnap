<template>
  <header>
    <div class="header">
      <img src="~/assets/img/logo.svg"/>
    </div>
  </header>
</template>

<script>

export default {
  name: "Header",
}
</script>

<style lang="scss" scoped>

.header{
  height: 70px;
  @include flexbox();
  @include align-items(center);
  @include justify-content(center);
}

</style>
