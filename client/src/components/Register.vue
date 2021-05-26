<template>
  <div>
    <h1>Register</h1>
    <div class="col-md-6 m-auto">
        <b-form-group label="Email address:">
          <b-form-input type="email" name="email" v-model="email" placeholder="email" required></b-form-input>
        </b-form-group>

        <b-form-group label="Password:">
          <b-form-input type="password" name="password" v-model="password" placeholder="password" required></b-form-input>
        </b-form-group>
        <div v-html="error" class="error">{{ error }}</div>
        <b-button @click="register" class="mt-3" variant="primary">Submit</b-button>
    </div>
  </div>
</template>

<script>
import AuthenticationService from '@/services/AuthenticationService'

export default {
  data () {
    return {
      email: '',
      password: '',
      error: null
    }
  },
  methods: {
    async register () {
      try {
        const response = await AuthenticationService.register({
          email: this.email,
          password: this.password
        })
        console.log(response.data)
      } catch (err) {
        this.error = err.response.data.error
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.error {
  color: red;
}
</style>
