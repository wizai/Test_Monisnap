<template>
  <div class="block-recipient">
    <div class="block-recipient__avatar">
      <img src="~/assets/img/avatar01.svg" class="block-recipient__avatar--img"/>
      <img src="~/assets/img/flag01.png" class="block-recipient__avatar--flag"/>
    </div>
    <div class="block-recipient__infos">
      <p class="block-recipient__infos--name">{{ recipient.firstname }} {{recipient.lastname}}</p>
      <p class="block-recipient__infos--amount" v-if="transfers.number">{{transfers.number}} tranferts</p>
    </div>
    <div class="block-recipient__btn btn" v-if="transfers.amount">
      Envoyer {{transfers.amount}}€
    </div>
  </div>
</template>

<script>
export default {
  name: "block-recipient",
  props: {
    recipient: {
      type: Object
    },
    transfers: {
      type: Object
    },
  },
}
</script>

<style lang="scss" scoped>

.block-recipient{
  background-color: $beige;
  padding: 12px;
  border-radius: 10px;
  opacity: 0;
  @include flexbox();
  @include align-items(center);
  @include justify-content(space-between);
  @include flex-flow(row wrap);
  @include animation( moveTextTop 1.5s cubic-bezier(0.2, 1, 0.3, 1) forwards);
  @for $i from 1 to 50 {
    &:nth-child(#{$i}) {
      animation-delay: $i * 0.15s;
    }
  }
  &__avatar{
    position: relative;
    &--img{
      max-width: 72px;
    }
    &--flag{
      position: absolute;
      top: 0;
      right: 0;
      max-width: 24px;
    }
  }
  &__infos{
    padding-left: 12px;
    max-width: calc(100% - 250px);
    @include flex-grow(1);
    &--name{
      font-weight: 600;
      margin-bottom: -8px;
      @include text-truncate();
    }
    &--amount{
      font-size: 12px;
    }
  }
  &__btn{
    text-align: right;
    margin-left: auto;
    @include flex-shrink(0)
  }
}

</style>
