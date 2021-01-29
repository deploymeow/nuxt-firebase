<template>
  <div>
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <nuxt-link class="navbar-brand" to="/">Vue Firebase</nuxt-link>
      <button
        class="navbar-toggler"
        type="button"
        data-toggle="collapse"
        data-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>

      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav mr-auto">
          <li class="nav-item">
            <nuxt-link class="nav-link" to="/">Home</nuxt-link>
          </li>
        </ul>
        <ul class="navbar-nav mr-0">
          <li v-if="!authenticatedUser" class="nav-item">
            <nuxt-link class="nav-link" to="/signin">Sign in</nuxt-link>
          </li>
          <li v-if="!authenticatedUser" class="nav-item">
            <nuxt-link class="nav-link" to="/signup">Register</nuxt-link>
          </li>
          <li v-else class="nav-item">
            <a class="logout nav-link" @click="signOut"
              >{{ user.email }} (Log out)</a
            >
          </li>
        </ul>
      </div>
    </nav>
    <nuxt />
  </div>
</template>

<script>
import * as firebase from "firebase/app";
import "firebase/auth";

export default {
  data() {
    return {
      user: null,
      authenticatedUser: null,
    };
  },
  created() {
    this.$fire.auth.onAuthStateChanged((user) => {
      this.user = user;
      this.authenticatedUser = user;
    });
  },
  methods: {
    async signOut() {
      await this.$fire.auth
        .signOut()
        .then(() => {
          console.log("success on signout");
        })
        .catch((e) => {
          console.log(e);
        });
    },
  },
};
</script>

<style scoped>
.logout {
  cursor: pointer;
}
</style>