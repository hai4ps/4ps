// src/components/SignIn.vue
<template>
  <div>
    <h2>Sign In</h2>
    <div class='formcontainer'>
      <input placeholder='Username' v-model='form.username' class='input' />
      <input placeholder='Password' type='password' v-model='form.password' class='input' />
      <button v-on:click='signIn' class='button'>Sign In</button>
      <button v-on:click="facebooksignIn">Sign In with Facebook</button>
      <button v-on:click="googlesignIn">Sign In with Google</button>
    </div>
  </div>
</template>

<script>
import { Auth } from 'aws-amplify'
import { AmplifyEventBus } from 'aws-amplify-vue'
export default {
  name: 'home',
  data() {
    return {
      form: {
        username: '',
        password: ''
      }
    }
  },
  methods: {
    async signIn() {
      const { username, password } = this.form
      await Auth.signIn(username, password)
      AmplifyEventBus.$emit('authState', 'signedIn')
      this.$router.push('/profile')
    },
   facebooksignIn: async function() {
      await Auth.federatedSignIn({provider: 'Facebook'});
    },
   googlesignIn: async function() {
      await Auth.federatedSignIn({provider: 'Google'}); 
    } 
  }
}
</script>
