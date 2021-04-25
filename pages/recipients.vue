<template>
  <section class="page_recipients">
    <BlockRecipients v-for="recipient in recipients" :key="recipient.id" :recipient="recipient"
                     :transfers="getTransfersByRecipient(recipient.id)">
    </BlockRecipients>
  </section>
</template>

<script>

import BlockRecipients from "~/components/block-recipient.vue";

export default {
  name: "recipients",
  data: function () {
    return {
      recipients: [],
      transfers: []
    }
  },
  components: {
    BlockRecipients,
  },

  async asyncData({ $axios, $config }) {
    const recipients = await $axios.$get('https://my-json-server.typicode.com/Monisnap/test-front-back/recipients')
    const transfers = await $axios.$get('https://my-json-server.typicode.com/Monisnap/test-front-back/transfers')
    return { transfers : transfers, recipients : recipients }
  },
  methods: {
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

.page_recipients {
  @include flexbox();
  @include justify-content(space-between);
  @include flex-flow(row wrap);
}

.block-recipient {
  width: calc(50% - 6px);
  margin-bottom: 12px;
  text-align: center;
  @include justify-content(center);
  @include flex-flow(column wrap);

  ::v-deep &__avatar {
    &--img {
      max-width: 120px;
    }

    &--flag {
      max-width: 36px;
    }
  }

  ::v-deep &__infos {
    padding-left: 0;
    max-width: 100%;
    margin-bottom: 15px;
  }

  ::v-deep &__btn {
    margin-right: auto;
  }
}

</style>
