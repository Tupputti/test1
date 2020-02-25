<template>
  <v-col class="mx-auto" :cols="8">
    <v-card class>
      <v-card-actions>
        <div class="flex-grow-1"></div>
        <v-card-text>Store Check</v-card-text>
        <!-- get ข้อมูล -->
        <v-dialog v-model="dialogcom" width="600px">
          <template v-slot:activator="{ on }">
            <v-btn icon v-on="on">
              <v-icon>mdi-chat</v-icon>
            </v-btn>
          </template>
          <div>
            <v-card v-for="get in UserList" :key="get">
              <v-container>
                <v-row>
                  <v-col>
                    <v-card>
                      <v-card-title class="fill-height align-end">{{get.Nicname}}</v-card-title>
                      <v-divider></v-divider>
                      <v-card-actions>
                        <div class="flex-grow-1"></div>
                        <v-card-text>{{get.Text}}</v-card-text>
                        <v-icon small class="mr-2" @click="editItem(item)">edit</v-icon>
                        <v-icon small @click="deleteItem(item)">delete</v-icon>
                      </v-card-actions>
                    </v-card>
                  </v-col>
                </v-row>
              </v-container>
            </v-card>
          </div>
        </v-dialog>
      </v-card-actions>
      <v-card-actions>
        <div class="flex-grow-1"></div>
        <v-card-text>Store Update</v-card-text>
        <!-- get ข้อมูล -->
        <v-dialog v-model="dialog" persistent max-width="600px">
          <template v-slot:activator="{ on }">
            <v-btn icon v-on="on">
              <v-icon>mdi-alert-circle-outline</v-icon>
            </v-btn>
          </template>
          <v-card>
            <v-card-title>
              <span class="headline">Comment</span>
            </v-card-title>
            <v-form ref="form" v-model="valid" lazy-validation>
              <v-container>
                <v-row>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field v-model="Nicname" label="Nicname*" required></v-text-field>
                  </v-col>
                  <v-col cols="12">
                    <v-text-field v-model="Text" label="Text*" required></v-text-field>
                  </v-col>
                </v-row>
              </v-container>
              <v-card-actions>
                <v-btn
                  color="success"
                  class="mr-4"
                  @click="addMember(),dialog = false,reloadPage()"
                >Save</v-btn>
                <v-btn color="blue" class="mr-4" @click="dialog = false">Close</v-btn>
              </v-card-actions>
            </v-form>
          </v-card>
        </v-dialog>
      </v-card-actions>
    </v-card>
  </v-col>
</template>

<script>
import firebase from 'firebase/app'
import 'firebase/auth'
import { db } from '@/plugins/firebaseConfig.js'
export default {
  data() {
    return {
      dialog: false,
      UserList: [],
      valid: false,
      Nicname: '',
      Text: '',
      cards: []
    }
  },
  editItem (item) {
        this.editedIndex = this.desserts.indexOf(item)
        this.editedItem = Object.assign({}, item)
        this.dialog = true
      },
      
  created() {
    this.getUser()
  },
  methods: {
    reloadPage() {
      window.location.reload()
    },
    addMember() {
      db.collection('store')
        .doc(this.Nicname)
        .set({
          Nicname: this.Nicname,
          Text: this.Text
        })
        .then(function(docRef) {
          //  console.log("Document written with ID: ", docRef.id);
        })
        .catch(err => {
          alert('Opps. ' + err.message)
        })
    },
    getUser() {
      db.collection('store')
        .get()
        .then(querySnapshot => {
          querySnapshot.forEach(doc => {
            // doc.data() is never undefined for query doc snapshots
            console.log(`${doc.Nicname} => ${doc.data()}`)
            this.UserList.push(doc.data())
          })
        })
    },
    reset() {
      this.$refs.form.reset()
    }
  }
}
</script>

<style>
</style>