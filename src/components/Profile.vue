// src/components/Profile.vue

<template>
  <h1>Welcome, {{user.attributes.identities}} {{user.attributes.email}}</h1>
</template>

<script>
import { Auth } from 'aws-amplify'

export default {
  name: 'Profile',
  data() {
    return {
      user: {}
    }
  },
  beforeCreate() {
    Auth.currentAuthenticatedUser()
      .then(user => { 
        this.user = user;
       console.log(user);})
      .catch(() => console.log('not signed in...'))
  }
}
</script>

