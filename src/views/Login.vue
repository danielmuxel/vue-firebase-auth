<template>
  <div class="columns">
    <div class="column">
      <div class="box is-shadowless">
        <h1 class="title">Hello and welcome back!</h1>
        <p>Just login to access your Dashboard again</p>
      </div>
    </div>
    <div class="column">
      <form class="box" @submit.prevent="submit">
        <h2 class="title">Login</h2>

        <article v-if="error" class="message is-danger">
          <div class="message-body">
            {{ error }}
          </div>
        </article>

        <div class="field">
          <label class="label">Email</label>
          <div class="control">
            <input v-model="form.email" class="input" type="text" />
          </div>
        </div>

        <div class="field">
          <label class="label">Password</label>
          <div class="control">
            <input v-model="form.password" class="input" type="password" />
          </div>
        </div>

        <div class="field is-grouped">
          <div class="control">
            <button type="submit" class="button is-link">Login</button>
          </div>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import firebase from "firebase";

export default {
  data() {
    return {
      form: {
        name: "",
        email: "",
        password: "",
      },
      error: null,
    };
  },
  methods: {
    submit() {
      firebase
        .auth()
        .signInWithEmailAndPassword(this.form.email, this.form.password)
        .then((data) => {
          this.$router.replace({ name: "Dashboard" });
        })
        .catch((err) => {
          this.error = err.message;
        });
    },
  },
};
</script>