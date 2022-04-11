<template>
    <v-form
    ref="form"
    v-model="valid"
    lazy-validation
    @submit.prevent="onSubmit"
  >
    <v-text-field
      v-model="nombre"
      :counter="20"
      :rules="nameRules"
      label="Name"
      required
    ></v-text-field>

    <v-text-field
      v-model="email"
      :rules="emailRules"
      label="E-mail"
      required
    ></v-text-field>

    <v-checkbox
      v-model="checkbox"
      label="Deseas recibir nuestro Newsletter?"
    ></v-checkbox>

    <v-btn
      type="submit"
      :disabled="!valid"
      color="success"
      class="mr-4"
    >
      Enviar
    </v-btn>

    <v-btn
      color="error"
      class="mr-4"
      @click="reset"
    >
      Resetear
    </v-btn>
  </v-form>
  <tabla-datos :lista="listaUsu"/>
</template>

<script>
import TablaDatos from './TablaDatos.vue';
import {ref,reactive} from 'vue'
export default {
    components: {
      TablaDatos
    },
    setup(){
      let valid= true
      let nombre=ref('')
      const nameRules= reactive([
        v => !!v || 'Name is required',
        v => v.length <= 20 || 'Name must be less than 20 characters',
        v => /^[A-Za-z]+([ A-Za-z])/.test(v) || 'Solo letras'
      ])
      let email= ref('')
      const emailRules= reactive([
        v => !!v || 'E-mail is required',
        v => /.+@.+\..+/.test(v) || 'E-mail must be valid',
      ])
      let checkbox= ref(false)
      let listaUsu=reactive(JSON.parse(localStorage.getItem("usuarios"))||[])
      //sin coma antes del return
      return{
        valid,nombre,nameRules, email,emailRules,checkbox,listaUsu
      }
    },
    methods:{
      validate () {
        this.$refs.form.validate()
                this.valid=true;
      },
      reset () {
        this.$refs.form.reset();
        this.valid=true;
      },
      onSubmit(){
        console.log("enviando")
        const nuevoUsu={
              nombre:this.nombre,
              email:this.email,
              suscripto:this.checkbox==true
          };
        this.listaUsu.push(nuevoUsu);
        localStorage.setItem("usuarios",JSON.stringify(this.listaUsu));
        this.valid=true;
      }
    }

}
</script>