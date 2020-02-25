<template>
  <div >
  </div>
</template>

<script>
import firebase from 'firebase/app'
import 'firebase/auth'
import { db } from '@/plugins/firebaseConfig'
export default {
  data() {
    return {
      userList: [],
      email: null,
      disbleSingin: false,
      disbleSingout: false,
      userName: '',
      tokenG: '',
    }
  },
  methods: {
    singin() {
     firebase.auth().signInWithCustomToken(token).catch((error) => {
  // Handle Errors here.
  var errorCode = error.code;
  var errorMessage = error.message;
  // ...

          this.email = user.email
          this.userName = user.displayName
          this.disbleSingin = true
          this.disbleGet = true
        //   this.$router.replace('/')
        })
        .catch((error) => {
          alert('Opps. ' + err.message)
        })
    }, 
  }
}
</script>

<style>
</style>