<template>
  <v-app>
    <v-app-bar fixed app>
      <div class="my-2">
        <span class="primary--text">AM3T'auto</span>
      </div>
      <div class="my-2">
        <v-btn class="ml-5" to="/product" text large color="primary">บริการ</v-btn>
      </div>
      <div class="my-2">
        <v-btn to="/list" text large color="primary">รายการซ่อม</v-btn>
      </div>
        
      <v-spacer />
     
    <div class="my-2"  :right="right" temporary fixed>
        <v-btn to="/check" text large color="primary" >สำหรับพนักงาน</v-btn>
      </div>
      <div class="my-2"  :right="right" temporary fixed>
        <v-btn to="/contact/" text large color="primary" >ติดต่อ</v-btn>
      </div>
      <div class="my-2"  :right="right" temporary fixed>
        <v-btn to="/" text large color="primary" >login</v-btn>
      </div>
      <!-- <login /> -->

    <!-- <v-btn @click="singout()" color="warning" class="ml-5">SingOut</v-btn> -->
      
     
    </v-app-bar>
    
    <v-content>
      <v-container>
        <nuxt />
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
import login from '~/components/login'
export default {
  components: {
    login,
  },
  data () {
    return {
      
    }
  }
}
</script>
