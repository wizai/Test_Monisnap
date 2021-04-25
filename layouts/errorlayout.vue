<template>
  <div class="layout error">
    <nuxt/>
  </div>
</template>

<script>
export default {
  // layoutTransition: 'layout',
  // or
  layoutTransition: {
    name: 'layout',
    mode: 'out-in'
  }
}
</script>

<style>
.layout-enter-active, .layout-leave-active {
  transition:all .8s cubic-bezier(.55,0,.1,1);
}
.layout-enter, .layout-leave-active {
  opacity: 0
}
</style>
