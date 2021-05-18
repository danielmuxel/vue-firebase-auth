<template>
  <h1>Register</h1>

  <div v-if="error">{{ error }}</div>

  <form @submit.prevent="submit">
    <label>Name</label>
    <input v-model="form.name" id="name" type="text" />

    <label>Email</label>
    <input v-model="form.email" id="email" type="text" />

    <label>Password</label>
    <input v-model="form.password" id="password" type="password" />

    <button type="submit">Register</button>
  </form>
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
        .createUserWithEmailAndPassword(this.form.email, this.form.password)
        .then((data) => {
          data.user.updateProfile({
            displayName: this.form.name,
          });
        })
        .catch((err) => {
          this.error = err.message;
        });
    },
  },
};
</script>