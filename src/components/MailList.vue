<template>
  <div class="container">
    <br />
    <div class="box" v-if="!emails.length">
      <p>There is not any email yet.</p>
    </div>
    <div class="mcard" v-for="email in emails" :key="email.id">
      <mail-card :email="email" @markAsRead="markAsRead" @archived="archived" />
    </div>
  </div>
</template>

<script>
import MailCard from '@/components/MailCard'
import axios from 'axios'
export default {
  name: 'MailList',
  data() {
    return {
      emails: [],
    }
  },
  props: {
    mailbox: String,
  },
  components: {
    MailCard,
  },
  mounted() {
    this.getEmails(this.mailbox)
    console.log(`mounted`)
    document.title = 'Mail ' + this.mailbox
  },
  methods: {
    async getEmails(mailbox) {
      this.$store.commit('setIsLoading', true)
      await axios
        .get('/api/v1/emails/' + mailbox)
        .then((response) => {
          this.emails = response.data
        })
        .catch((error) => {
          console.log(`error`, error)
        })
      this.$store.commit('setIsLoading', false)
    },
    async markAsRead(email) {
      await axios
        .put(`/api/v1/email/${email.id}`, {
          read: !email.read,
        })
        .then(() => {
          email.read = !email.read
        })
        .catch((error) => {
          console.log(`error`, error)
        })
    },
    async archived(email) {
      await axios
        .put(`/api/v1/email/${email.id}`, {
          archived: !email.archived,
        })
        .then(() => {
          email.archived = !email.archived
          this.emails = this.emails.filter((e) => e.id != email.id)
        })
        .catch((error) => {
          console.log(`error`, error)
        })
    },
  },
}
</script>
