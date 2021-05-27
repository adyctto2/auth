<template>
<div class="login">
  <br> 
  <v-card
    class="mx-auto align-center"
    max-width="450"
    elevation="9"
  >
    <v-img
      src="../assets/logo.jpg"
      :max-width="width"
      class="logo"
    ></v-img>
    <h2 class="text-center"><strong> Autenticación </strong></h2>
    <v-card-text >
          <v-text-field
              ref="name"
              v-model="name"
              :rules="[() => !!name || 'Este campo es requerido']"
              :error-messages="errorMessages"
              label="Ingrese su usuario"
              placeholder="Ingrese su usuario"
              required
          ></v-text-field>
          <v-text-field
              v-model="password"
              :append-icon="show1 ? 'mdi-eye' : 'mdi-eye-off'"
              :rules="[rules.required, rules.min]"
              :type="show1 ? 'text' : 'password'"
              name="input-10-1"
              label="Ingrese su contraseña"
              hint="8 caracteres como minimo"
              counter
              id="password"
              @click:append="show1 = !show1"
            ></v-text-field>
      </v-card-text>

      <v-card-actions>
        <div class="logo">
          <v-btn
          color="cyan darken-1"
          @click="sendLogin()"
        >
          <v-icon left>
            mdi-key
          </v-icon> Iniciar Sesión
        </v-btn>
        </div>

      </v-card-actions>
    <!-- <v-card-text>
      <v-alert
        v-model="alert"
        close-text="Close Alert"
        type="error"
        dark
        dismissible
      >
      Error de autenticacion</v-alert>
    </v-card-text> -->
    <br>
    <!-- <p class="tex}t-center">(- * -)</p> -->
    <!-- <h4 class="text-center">Ingresa con</h4>
    <v-card-text elevation="9" >
        <a href="" class="accion" block>
            <v-img class="logo "
            src="../assets/logo_ciudadania_digital.png"
            width="50%"
            ></v-img>
        </a>
    </v-card-text> -->
    <v-card-text>
      <v-row>
        <v-col>
          <a href="" block>¿Se te olvido tu contraseña?</a>

        </v-col>
        <v-col>
          <a href="" block>Solicita ciudadania digital</a>

        </v-col>
      </v-row>

    </v-card-text>
  </v-card>
</div>
</template>

<script>
import axios from 'axios';
  export default {
    name: 'Login',
    data: () => ({
      show: false,
      width : '70%',
      show1: false,
      password: '',
      name: '',
      alert : '',
      errorMessages : '',
      rules: {
        required: value => !!value || 'Requerido.',
        min: v => v.length >= 8 || 'Min 8 caracteres',
        emailMatch: () => (`The email and password you entered don't match`),
      },
    }),
    components: {
    },
    methods:{
      async sendLogin(){
        console.log(this.password+" "+this.name);
        try {
             const resp=await axios.post(`http://jsonplaceholder.typicode.com/posts`, {
              body: {
                'name' : this.name,
                'password' : this.password
              }
            })
            if(resp.status === '200'){
              if(resp.validado){
                console.log("Inicio de sesion correcto!!")
              }
              else{
                this.errorMessages = resp.error;
              }
            }
          } catch (e) {
            this.errors.push(e)
          }
      }
    }
  }
</script>
<style>
  .logo{
    display: block; margin: auto;
  }
  .acccion{
    border: 1px solid black imp !important;
  }
  .acccion:hover{
    opacity: 0.5 imp !important;
  }
</style>
