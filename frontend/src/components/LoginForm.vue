<template>
  <div id="login-form">
    <form>
      <label>Username</label>
      <input v-model="user.username" type="text" />
      <label>Password</label>
      <input v-model="user.password" type="password" />
      <button @click="handleLogin()">Login</button>
      <button @click="handleHello()">Hello</button>
    </form>
  </div>
</template>

<script>
  import api from "./backend-api";

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
          this.response = response.data;
          console.log('Created new User with Id ' + response.data);
        })
        .catch(e => {
          this.errors.push(e)
        });
      },
      
      handleHello() {
        api.hello()
        .then(response => {
          console.log('1');
          this.response = response.data;
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