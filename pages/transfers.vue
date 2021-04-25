<template>
  <section>
    <BlockTransfer v-for="transfer in transfers" :key="transfer.id" :transfer="transfer"
                   :recipient="getRecipientByTransfer(transfer.recipient)">
    </BlockTransfer>
  </section>
</template>

<script>

import BlockTransfer from "~/components/block-transfer.vue";

export default {
  name: "transfers",
  data: function () {
    return {
      recipients: [],
      transfers: []
    }
  },
  components: {
    BlockTransfer,
  },

  async asyncData({ $axios, $config }) {
    const recipients = await $axios.$get('https://my-json-server.typicode.com/Monisnap/test-front-back/recipients')
    const transfers = await $axios.$get('https://my-json-server.typicode.com/Monisnap/test-front-back/transfers')
    return { transfers : transfers, recipients : recipients }
  },

  methods: {
    getRecipientByTransfer(id) {
      if (this.recipients.length) {
        return this.recipients.filter(recipient => recipient.id === id)
      }
    },
  },
}
</script>

<style lang="scss">

.block-transfer {
  margin-bottom: 12px;
}

</style>
