<template>
    <v-flex xs12 sm6 offset-sm3 mt-3>
      <form>
        <v-layout column>
          <v-flex xs12 class="mx-auto" mt-5>
      <h3>Log In</h3>
    </v-flex>
          <v-flex class="auto">
            <v-text-field
              name="email"
              label="Email"
              id="email"
              type="email"
              required></v-text-field>
          </v-flex>
          <v-flex class="auto">
            <v-text-field
              name="password"
              label="Password"
              id="password"
              type="password"
              required></v-text-field>
          </v-flex>
          <v-flex  mt-5>
            <v-btn class="mx-auto"  type="submit">Login</v-btn>
            <v-btn to="/singup" class="mx-auto" text large color="primary">Sing Up</v-btn>
          </v-flex>
        </v-layout>
      </form>
    </v-flex>
</template>

<script>
import firebase from 'firebase/app'
import 'firebase/auth'
import { db } from '@/plugins/firebaseConfig'
import login from '~/components/login'
  export default {
  components: {
    login,
  },
    props: {
      source: String,
    },
  data() {
    return {
      userList: [],
      email: null,
      disbleSingin: false,
      disbleSingout: false,
      userName: '',
      tokenG: '',
      drawer: null,
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