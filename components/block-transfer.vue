<template>
  <div class="block-transfer" v-if="transfer">
    <div class="block-transfer__avatar">
      <img v-if="transfer.country === 'MA'" src="~/assets/img/avatar01.svg" class="block-transfer__avatar--img"/>
      <img v-else src="~/assets/img/avatar08.svg" class="block-transfer__avatar--img"/>
      <img v-if="transfer.country === 'MA'" src="~/assets/img/flag01.png" class="block-transfer__avatar--flag"/>
      <img v-else src="~/assets/img/flag08.png" class="block-transfer__avatar--flag"/>
    </div>
    <div class="block-transfer__infos">
      <p class="block-transfer__infos--name" v-if="recipient[0].firstname && recipient[0].lastname">{{ recipient[0].firstname }} {{ recipient[0].lastname }}</p>
      <p class="block-transfer__infos--amount" v-if="transfer.amount">{{ transfer.amount }} EUR</p>
    </div>
    <div class="block-transfer__received">
      <p class="block-transfer__received--title" v-if="transfer.status === 'SUCCESS'">Reçu</p>
      <p class="block-transfer__received--title" v-else>Echec</p>
      <p class="block-transfer__received--date" v-if="transfer.date">{{ $moment(transfer.date).format("DD MMMM YYYY") }}</p>
    </div>
    <button v-if="transfer.status === 'SUCCESS'" class="block-transfer__btn btn">
      Refaire l'envoi
    </button>
    <button v-else class="block-transfer__btn btn btn_red">
      L'envoi à échoué
    </button>
  </div>
</template>

<script>
export default {
  name: "block-transfer",
  props: {
    transfer: {
      type: Object
    },
    recipient: {
      type: Array
    },
  },
}
</script>

<style lang="scss" scoped>

.block-transfer{
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
    height: 72px;
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
    max-width: calc(100% - 180px);
    @include flex-grow(1);
    &--name{
      margin-bottom: -8px;
      font-weight: 600;
      @include text-truncate();
    }
    &--amount{
      font-weight: 700;
      font-size: 20px;
      font-family: $SpaceGrotesk;
    }
  }
  &__received{
    text-align: right;
    font-size: 12px;
    margin-left: auto;
    &--title{
      font-weight: 600;
    }
    &--date{
      opacity: .6;
    }
  }
  &__btn{
    width: 100%;
    margin-top: 12px;
    @include flex-shrink(0)
  }
}

</style>
