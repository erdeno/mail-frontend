<template>
  <div class="container">
    <br />
    <div class="column mb0" v-for="email in emails" :key="email.id">
      <mail-card />
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import MailCard from '@/components/MailCard'
export default {
  name: 'Home',
  data() {
    return {
      emails: [],
    }
  },
  components: {
    MailCard,
  },
  mounted() {
    this.getEmails()
    document.title = 'Mail'
  },
  methods: {
    async getEmails() {
      this.$store.commit('setIsLoading', true)

      await axios
        .get('/api/v1/emails/inbox')
        .then((response) => {
          this.emails = response.data
        })
        .catch((error) => {
          console.log(`error`, error)
        })
      this.$store.commit('setIsLoading', false)
      console.log(`emails`, this.emails)
    },
  },
}
</script>
