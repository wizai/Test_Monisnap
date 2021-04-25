<template>
  <section>
    <div class="block-history">
      <h2>Mon historique</h2>
      <div class="block-history__container">
        <div class="block-history__item">
          <p class="block-history__item--number">{{ getNumberOfTransfers() }}</p>
          <p class="block-history__item--txt">transferts</p>
        </div>
        <div class="block-history__item">
          <p class="block-history__item--number">{{ getNumberOfRecipients() }}</p>
          <p class="block-history__item--txt">bénéficiaires</p>
        </div>
        <div class="block-history__item">
          <p class="block-history__item--number">{{ getNumberOfTransfersSuccess() }}</p>
          <p class="block-history__item--txt">envoyés</p>
        </div>
        <div class="block-history__item">
          <p class="block-history__item--number">
            <img v-if="favorite.destination === 'MA'" src="~/assets/img/flag01.png"/>
            <img v-else src="~/assets/img/flag08.png"/>
          </p>
          <p class="block-history__item--txt">destination favorite</p>
        </div>
      </div>
    </div>
    <div class="block-lastTransfer">
      <h2>Mon dernier transfert</h2>
      <BlockTransfer :transfer="transfers[0]" :recipient="getRecipientByTransfer(transfers[0].recipient)"/>
      <div class="block-lastTransfer__link">
        <nuxt-link
          to="/transfers"
          exact
        >Voir tous mes transferts
        </nuxt-link>
      </div>
    </div>
    <div class="block-favorite">
      <h2>Mon bénéficiaire favori</h2>
      <BlockRecipient :recipient="recipients[favorite.index]"
                      :transfers="getTransfersByRecipient(favorite.id)"/>
      <div class="block-favorite__link">
        <nuxt-link
          to="/recipients"
          exact
        >Voir tous mes bénéficiaires
        </nuxt-link>
      </div>
    </div>
  </section>
</template>

<script>

import BlockTransfer from "~/components/block-transfer.vue";
import BlockRecipient from "~/components/block-recipient.vue";
import transfers from "./transfers";

export default {
  data() {
    return {
      recipients: [],
      transfers: [],
      favorite : {}
    }
  },
  components: {
    BlockTransfer,
    BlockRecipient
  },

  async asyncData({ $axios, $config }) {
    const recipients = await $axios.$get('https://my-json-server.typicode.com/Monisnap/test-front-back/recipients')
    const transfers = await $axios.$get('https://my-json-server.typicode.com/Monisnap/test-front-back/transfers')
    return { transfers : transfers, recipients : recipients }
  },

  created() {
    this.getFavoriteRecipientId();
    this.getFavoriteDestination();
  },

  methods: {
    getRecipientByTransfer(id) {
      if (this.recipients.length) {
        return this.recipients.filter(recipient => recipient.id === id)
      }
    },
    getFavoriteRecipientId() {
      // Create an array with only transfer with property status is good and after get the value with the highest occurrence + index
      const arr = this.transfers.filter(transfer=>transfer.status === 'SUCCESS').map(transfer=>transfer.recipient);
      this.favorite.id = arr.reduce(
        (a,b,i,arr)=>
          (arr.filter(v=>v===a).length>=arr.filter(v=>v===b).length?a:b),
        null)
      this.favorite.index =  arr.indexOf(this.favorite.id)
    },
    getNumberOfTransfers(){
      return this.transfers.length;
    },
    getNumberOfRecipients(){
      return this.recipients.length;
    },
    getNumberOfTransfersSuccess(){
      let counter = 0;
      let $this = this;
      for (const transfer of $this.transfers) {
        if (transfer.status === 'SUCCESS') counter += 1;
      }
      return counter;
    },
    getFavoriteDestination(){
      // Create an array with only country with property status is good and after get the value with the highest occurrence + index
      const arr = this.transfers.map(transfer=>transfer.country);
      this.favorite.destination = arr.reduce(
        (a,b,i,arr)=>
          (arr.filter(v=>v===a).length>=arr.filter(v=>v===b).length?a:b),
        null)
    },
    getTransfersByRecipient(id) {
      if (this.transfers.length){
        const data = this.transfers.filter(transfer => transfer.recipient === id)
        return {
          number: data.length,
          amount: data.map(data => data.amount).reduce((prev, next) => prev + next)
        }
      }
    },
  },
}
</script>

<style lang="scss" scoped>

section{
  & > div {
    opacity: 0;
    @include animation( moveTextTop 1.5s cubic-bezier(0.2, 1, 0.3, 1) forwards);
    @for $i from 1 to 50 {
      &:nth-child(#{$i}) {
        animation-delay: $i * 0.15s;
      }
    }
  }
}

.block-history {
  margin-bottom: 30px;
  &__container {
    @include flexbox();
    @include align-items(stretch);
    @include justify-content(space-between);
    @include flex-flow(row wrap);
  }

  &__item {
    border-radius: 10px;
    width: calc(50% - 6px);
    background-color: rgba(102, 102, 255, .1);
    height: 100px;
    margin-bottom: 12px;
    @include flexbox();
    @include align-items(center);
    @include justify-content(center);
    @include flex-flow(column wrap);

    &--number {
      font-family: $SpaceGrotesk;
      font-weight: 700;
      font-size: 36px;
      line-height: 28px;
    }

    &--txt {
      font-size: 16px;
    }
  }
}

.block-lastTransfer, .block-favorite {
  margin-bottom: 30px;
  ::v-deep .block-transfer, ::v-deep .block-recipient{
    opacity: 1;
    @include animation(inherit)
  }
  &__link {
    margin-top: 12px;
    text-align: center;
    a{
      text-decoration: underline;
      color: $black;
      font-size: 12px;
    }
  }
}

</style>
