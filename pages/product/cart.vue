<template>
  <div class="container">
     <v-form ref="form" v-model="valid" lazy-validation>
        <v-text-field v-model="memberid" :counter="10" :rules="nameRules" label="รหัสลูกค้า" required></v-text-field>

        <v-btn :disabled="!valid" color="success" class="mr-4" @click="addMember()">Add Member</v-btn>

        <v-btn color="error" class="mr-4" @click="reset">Reset Form</v-btn>

        <v-btn color="warning" @click="resetValidation">Reset Validation</v-btn>
    </v-form>
    <center>
      <h1>Buy Product</h1>
      <h3 class="total">Total: ฿ {{ totalPrice() }}.00 THB</h3>
    </center>
    <br />
    <ul class="list-group">
      <li class="list-group-item my-sm-1" v-for="(product,index) in cart " :key="index">
        <center>
          <img  :src="product.image"  alt width="100px" height="100px" />
        </center>
          <v-select v-model="select" :items="items" :rules="[v => !!v || 'Item is required']" label="จังหวัด" required></v-select>
        <h5 >{{product.name}}</h5>
        <h5>price: {{product.price}} THB</h5>
        <button
          class="product-remove btn btn-outline-danger my-0 my-sm-5"
          @click="remove(index)"
        >ลบสินค้า</button>
      </li>
    </ul>
    <center>
      <div>
      <button class="product-remove btn btn-outline-info my-0 my-sm-5">สั่งซื้อ</button>
      </div>
    </center>
  </div>
</template>

<script>
import {db} from '@/plugins/firebaseConfig'


export default {
  data() {() => ({
        memberid: '',
        valid: true,
        name: '',
        nameRules: [
            v => !!v || 'Name is required',
            v => (v && v.length <= 10) || 'ใส่ชื่อได้ไม่เกิน 10 ตัวอักษร',
        ],
    });
    //   เรียกใช้ store ตาม foder
    return {
      cart: this.$store.state.product.cart
    };
  },
  methods: {
    addMember() {
                db.collection("Addmember").doc(this.memberid).set({
             memberid: this.memberid,
             select: this.select,
        })
        .then(function(docRef) {
            //  console.log("Document written with ID: ", docRef.id);
        })
        .catch(function(error) {
              console.error("Error adding document: ", error);
        });

        },

        validate() {
            if (this.$refs.form.validate()) {
                this.snackbar = true
            }
        },
        reset() {
            this.$refs.form.reset()
        }, 
    remove(cart) {
      this.$store.commit("product/removecart", cart);
    },
    totalPrice() {
      return this.$store.state.product.cart.reduce(
        (price, next) => price + next.price,
        0
      );
    }
  }
};
</script>

<style>
.list-group-item {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 1rem;
  text-align: center;
}
</style>