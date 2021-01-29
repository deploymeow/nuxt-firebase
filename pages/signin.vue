<template>
  <div class="container">
    <div class="d-flex justify-content-center flex-row">
      <div class="col">
        <div class="card">
          <div class="card-header">Sign in</div>
          <div class="card-body">
            <form @submit.prevent="signIn">
              <div class="form-group">
                <input
                  class="form-control email"
                  type="text"
                  v-model="email"
                  placeholder="Email"
                />
              </div>
              <div class="form-group">
                <input
                  class="form-control"
                  type="password"
                  v-model="password"
                  placeholder="Password"
                />
              </div>
              <button class="btn btn-primary btn-large" type="submit">
                Submit
              </button>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import * as firebase from "firebase/app";
import "firebase/auth";

export default {
  data() {
    return {
      email: "",
      password: "",
    };
  },
  methods: {
    async signIn() {
      try {
        await this.$fire.auth
          .signInWithEmailAndPassword(this.email, this.password)
          .then((user) => {
            console.log("Success on sign in");
            this.$router.push("/");
          });
      } catch (e) {
        alert(e);
      }
    },
  },
};
</script>

<style scoped>
.email {
    margin-top:30px;
}
.card {
  display: flex;
  margin: 0 auto;
  max-width: 500px;
}
input {
  display: flex;
  margin: 0 auto;
  max-width: 300px;
}
button {
  display: flex;
  margin: 0 auto;
  border-radius: 20px;
  background: primary;
}
</style>