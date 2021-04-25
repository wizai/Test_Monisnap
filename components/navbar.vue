<template>
  <div>
    <ul class="navbar">
      <li v-for="link in links" :key="link.id" class="navbar__item">
        <nuxt-link
          :to="{ path: link.url }"
          exact
          class="navbar__item--link"
        >
          <span class="material-icons navbar__item--picto">{{ link.icon }}</span>
          <span class="navbar__item--txt">{{ link.name }}</span>
        </nuxt-link>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "Navbar",
  data() {
    return {
      links: [
        {
          id: 1,
          name: "Accueil",
          url: "/",
          icon: "home"
        },
        {
          id: 2,
          name: "Transferts",
          url: "/transfers",
          icon: "swap_horiz"
        },
        {
          id: 3,
          name: "Bénéficaires",
          url: "/recipients",
          icon: "people"
        },
      ],
      open: false
    };
  },
}
</script>

<style lang="scss" scoped>

.navbar{
  position: relative;
  @include flexbox();
  @include justify-content(space-between);
  &:after{
    content: '';
    position: absolute;
    bottom: -10px;
    left: 0;
    width: 100%;
    height: 10px;
    background-color: $white;
    @include box-shadow(0px 0px 8px rgba(0, 0, 0, 0.25));
  }
  &__item{
    position: relative;
    width: calc(33.333% - 1px);
    &--link{
      position: relative;
      height: 72px;
      text-decoration: none;
      outline: none;
      color: rgba(10, 9, 10, .6);
      background-color: rgba(255, 255, 255, .7);
      border-top-right-radius: 10px;
      border-top-left-radius: 10px;
      @include flexbox();
      @include align-items(center);
      @include justify-content(center);
      @include flex-flow(column wrap);
      @include transition(all .25s ease-in-out);
      &.active{
        background-color: $white;
        z-index: 3;
        color: $blue;
        @include box-shadow(0px 0px 8px rgba(0, 0, 0, 0.25));
        clip-path: inset(-8px -8px 0px -8px);
      }
    }
    &--picto{
      font-size: 28px;
    }
    &--txt{
      font-size: 12px;
      font-weight: 400;
    }
  }
}

</style>
