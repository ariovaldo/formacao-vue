<template>
  <v-app>
    <v-card width="400px" class="mx-auto  my-auto" elevation="7" >
      <v-card-title class="teal lighten-2">
        <h1 class="display-1" >Login</h1>
      </v-card-title>
      <v-card-text class="mt-5">
        <v-alert type="error" :dense="true" v-show="valid && msg !=''"> 
            {{msg}}
        </v-alert>
        <v-form 
          ref="form"
          v-model="valid"
          lazy-validation
          elevation=5
          v-on:submit.prevent="login"
        >
          <v-text-field 
            label="Username" 
            prepend-icon = "mdi-account-circle"
            v-model="Username"
            name ="username"
            autocomplete="username"
            :rules="nameRules"
            :counter="10"
            required
          />
          <v-text-field 
            :type="showPassword?'text':'password'"
            label="Password" 
            v-model="Password"
            name ="Password"
            autocomplete="current-password"
            prepend-icon = "mdi-lock"
            :rules="nameRules"
            :append-icon = "showPassword ?'mdi-eye':'mdi-eye-off'" 
            @click:append="showPassword = !showPassword"
            required
          />
        </v-form>
      </v-card-text>
      <v-divider></v-divider>
      <v-card-actions>
        <v-btn 
          color="success darken-1" 
          @click="clear"
        >Register</v-btn>
        <v-spacer></v-spacer>
        <v-btn 
          color="teal lighten-2"
          @click="login"
          >Login</v-btn>
      </v-card-actions>
    </v-card>
  </v-app>
  
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  name: "App",

  components: { },

  data: () => ({
    showPassword:false,
    valid: true,
    Username: '',
    msg: '',
    Password:'',
    nameRules: [
      v => !!v || 'Name is required',
      v => (v && v.length <= 10) || 'Name must be less than 10 characters',
    ]
  }),

  methods: {
      login(){
        if(this.$refs.form.validate()){
          this.msg  = "Usuário ou senha  não encontrado."
        }else{
          //this.msg  = "Erro no form."
        }
      },
      clear() {
        this.$refs.form.reset()
        this.msg='';
      }
  }
});
</script>

<style>
 h1 {
   color:#000;
   text-shadow: 1px 1px rgba(0, 0, 0, 0.2);
 }
</style>

