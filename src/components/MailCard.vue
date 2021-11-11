<template>
  <div class="card">
    <header class="card-header" @click="showContent" style="user-select: none">
      <p class="card-header-title">
        {{ mail.subject }}
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
          from {{ mail.sender }}
          {{ mail.body }}
          <br />
          On
          <time>{{ mail.date }}</time>
        </div>
      </div>
      <footer class="card-footer">
        <a href="#" class="card-footer-item">Save</a>
        <a href="#" class="card-footer-item">Edit</a>
        <a href="#" class="card-footer-item">Delete</a>
      </footer>
    </div>
  </div>
</template>
<script>
export default {
  name: 'MailCard',
  data() {
    return {
      mail: {
        subject: 'Job application',
        sender: 'ceza@mail.com',
        date: '20 Oct 2021',
        body: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Phasellus nec iaculis mauris.',
      },
      displaying: false,
      icon: 'fas fa-angle-down',
    }
  },
  components: {},
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
  },
}
</script>

<style scoped>
.card {
  margin-bottom: 0px;
  padding: 0px;
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
