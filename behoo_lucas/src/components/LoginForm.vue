<template>
  <div id="login-form">
    <form>
      <label>Username</label>
      <input v-model="user.username" type="text" />
      <label>Password</label>
      <input v-model="user.password" type="password" />
      <button @click="handleLogin()">Login</button>
    </form>
  </div>
</template>

<script>
  import api from "../bk-api/login_apis";

  export default {
    name: 'Login-Form',
    data() {
      return {
        response: 1,
        errors: [],
        user: {
          username: '',
          password: '',
        },
      }
    },
    methods: {
      handleLogin() {
        api.auth(this.user.username, this.user.password)
          .then(response => {
            console.log(response.data);
          })
          .catch(e => {
            this.errors.push(e)
          });
      }
    }
  }
</script>

<style scoped>
  form {
    margin-bottom: 2rem;
  }
</style>
