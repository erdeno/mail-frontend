<template>
  <div class="card">
    <header class="card-header" @click="showContent">
      <p class="card-header-title">
        {{ email.subject }}
        <span class="tag is-primary is-light" v-if="!email.read">New</span>
      </p>
      <button class="card-header-icon" aria-label="more options">
        <span class="icon">
          <i :class="icon" aria-hidden="true"></i>
        </span>
      </button>
    </header>
    <div class="card-body" v-if="displaying">
      <div class="card-content">
        <div class="content">
          from {{ email.sender }}
          {{ email.body }}
          <br />
          On
          <time>{{ email.timestamp }}</time>
        </div>
      </div>
      <footer class="card-footer">
        <button class="card-footer-item button is-ghost" @click="read(email)">
          {{ email.read ? 'Unread' : 'Mark as Read' }}
        </button>
        <button class="card-footer-item button is-ghost">Forward</button>
        <button class="card-footer-item button is-ghost" @click="archive(email)">
          {{ email.archived ? 'Unarchive' : 'Archive' }}
        </button>
      </footer>
    </div>
  </div>
</template>
<script>
export default {
  name: 'MailCard',
  emits: ['markAsRead', 'archived'],
  data() {
    return {
      displaying: false,
      icon: 'fas fa-angle-down',
    }
  },
  props: {
    email: Object,
  },
  methods: {
    showContent() {
      if (!this.displaying) {
        this.displaying = true
        this.icon = 'fas fa-angle-up'
      } else {
        this.displaying = false
        this.icon = 'fas fa-angle-down'
      }
    },
    read(email) {
      this.$emit('markAsRead', email)
    },
    archive(email) {
      this.$emit('archived', email)
    },
  },
}
</script>

<style lang="scss" scoped>
.card {
  margin-bottom: 0;
  padding: 0px;
  border-radius: 0;
}
.card-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.text {
  font-size: 14px;
}

.item {
  margin-bottom: 18px;
}

.box-card {
  width: 600px;
}
</style>
