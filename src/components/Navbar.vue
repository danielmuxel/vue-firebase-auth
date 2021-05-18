<template>
  <nav class="navbar" role="navigation" aria-label="main navigation">
    <div class="navbar-brand">
      <router-link class="navbar-item" to="/">Vue-Firebase-Auth</router-link>

      <a
        role="button"
        class="navbar-burger"
        :class="{ 'is-active': isNavOpen }"
        aria-label="menu"
        aria-expanded="false"
        data-target="navbarBasicExample"
        @click="isNavOpen = !isNavOpen"
      >
        <span aria-hidden="true"></span>
        <span aria-hidden="true"></span>
        <span aria-hidden="true"></span>
      </a>
    </div>

    <div
      id="navbarBasicExample"
      class="navbar-menu"
      :class="{ 'is-active': isNavOpen }"
    >
      <div class="navbar-start">
        <router-link class="navbar-item" to="/"> Home </router-link>
        <router-link v-if="user.loggedIn" class="navbar-item" to="/dashboard"> Dashboard </router-link>
      </div>

      <template v-if="!user.loggedIn">
        <div class="navbar-end">
          <div class="navbar-item">
            <div class="buttons">
              <router-link to="/register" class="button is-primary">
                <strong>Sign up</strong>
              </router-link>
              <router-link to="/login" class="button is-light">
                Log in
              </router-link>
            </div>
          </div>
        </div>
      </template>
      <template v-else>
        <div class="navbar-end">
          <div class="navbar-item">
            <div class="buttons">
              <button @click.prevent="signOut" class="button is-primary">
                Logout
              </button>
            </div>
          </div>
        </div>
      </template>
    </div>
  </nav>
</template>

<script>
import { mapGetters } from "vuex";
import firebase from "firebase";

export default {
  data() {
    return {
      isNavOpen: false,
    };
  },
  computed: {
    ...mapGetters({
      // map `this.user` to `this.$store.getters.user`
      user: "user"
    })
  },
  methods: {
    signOut() {
      firebase
        .auth()
        .signOut()
        .then(() => {
          this.$router.replace({
            name: "home"
          });
        });
    }
  }
};
</script>