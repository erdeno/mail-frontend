<template>
  <mail-list mailbox="inbox" />
</template>

<script>
import MailList from '@/components/MailList'
export default {
  name: 'Home',
  components: {
    MailList,
  },
}
</script>
