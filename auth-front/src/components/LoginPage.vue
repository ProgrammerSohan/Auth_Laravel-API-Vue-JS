<template>
  <div class="row">
    <div class="col-sm-4">
      <h2 align="center">Login</h2>
      <form @submit.prevent="loginData">
        <div class="form-group" align="left">
          <label>Email</label>
          <input type="email" v-model="student.email" class="form-control" placeholder="Email">
        </div>
        <div class="form-group" align="left">
          <label>Password</label>
          <input type="password" v-model="student.password" class="form-control" placeholder="Password">
        </div>
        <button type="submit" class="btn btn-primary">Login</button>
      </form>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'LoginPage',
  data() {
    return {
      student: {
        email: '',
        password: ''
      }
    };
  },
  methods: {
    loginData() {
      axios.post("http://127.0.0.1:8000/api/login", this.student)
        .then(({ data }) => {
          console.log(data);
          try {
            if (data.status === true) {
              alert("Login Successfully");
             // this.$router.push({ name: 'HelloWorld' });
              this.$router.push({ name: 'SohanPage' });

            } else {
              alert("Login failed");
            }
          } catch (err) {
            alert("Error, please try again");
          }
        })
        .catch(error => {
          console.error("Error during login:", error);
          alert("Error during login. Please try again.");
        });
    }
  }
};
</script>

<style scoped>
/* Add your component-specific styles here */
</style>
