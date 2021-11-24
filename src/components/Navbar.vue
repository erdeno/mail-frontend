<template>
  <nav class="navbar" role="navigation" aria-label="main navigation">
    <div class="navbar-brand">
      <router-link class="navbar-item" to="/">
        <img :src="icon" width="112" height="28" />
      </router-link>

      <a
        class="navbar-burger"
        aria-label="menu"
        aria-expanded="false"
        data-target="navbar-menu"
        @click="showMobileMenu = !showMobileMenu"
      >
        <span aria-hidden="true"></span>
        <span aria-hidden="true"></span>
        <span aria-hidden="true"></span>
      </a>
    </div>

    <div class="navbar-menu" id="navbar-menu" :class="{ 'is-active': showMobileMenu }">
      <div class="navbar-start">
        <template v-if="$store.state.isAuthenticated">
          <router-link class="navbar-item" to="/">Inbox</router-link>
          <router-link class="navbar-item" to="/archived">Archived</router-link>
          <router-link class="navbar-item" to="/">Sent</router-link>
        </template>
      </div>

      <div class="navbar-end">
        <div class="navbar-item">
          <div class="buttons">
            <template v-if="$store.state.isAuthenticated">
              <button @click="logout()" class="button is-danger">Log out</button>
            </template>

            <template v-else>
              <router-link
                to="/sign-up"
                class="button"
                :class="activePage == '/sign-up' ? 'is-primary' : 'is-light'"
                >Sign up
              </router-link>
              <router-link
                to="/log-in"
                class="button"
                :class="activePage == '/log-in' ? 'is-primary' : 'is-light'"
                >Log in</router-link
              >
            </template>
          </div>
        </div>
      </div>
    </div>
  </nav>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Navbar',
  data() {
    return {
      showMobileMenu: false,
      icon: require('@/assets/logo.png'),
    }
  },
  methods: {
    logout() {
      axios.defaults.headers.common['Authorization'] = ''

      localStorage.removeItem('token')
      localStorage.removeItem('username')
      localStorage.removeItem('userid')

      this.$store.commit('removeToken')

      this.$router.push('/')
    },
  },
  computed: {
    activePage() {
      return this.$route.path
    },
  },
}
</script>
