<template>
  <v-form
    ref="form"
    v-model="valid"
    lazy-validation
    @submit.prevent="onSubmit"
  >
    <v-text-field
      v-model="name"
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
  export default {
    components: {
      TablaDatos
    },
    data: () => ({
      valid: true,
      name: '',
      nameRules: [
        v => !!v || 'Name is required',
        v => v.length <= 20 || 'Name must be less than 20 characters',
        v => /^[A-Za-z]+([ A-Za-z])/.test(v) || 'Solo letras'
      ],
      email: '',
      emailRules: [
        v => !!v || 'E-mail is required',
        v => /.+@.+\..+/.test(v) || 'E-mail must be valid',
      ],
      checkbox: false,
      listaUsu:JSON.parse(localStorage.getItem("usuarios"))||[],
    }),

    methods: {
      validate () {
        this.$refs.form.validate()
      },
      reset () {
        this.$refs.form.reset();
        this.valid=true;
      },
      onSubmit(){
        console.log("enviando")
        const nuevoUsu={
              nombre:this.name,
              celular:this.phoneNumber,
              email:this.email,
              suscripto:this.checkbox==this.checkbox
          };
        this.listaUsu.push(nuevoUsu);
        localStorage.setItem("usuarios",JSON.stringify(this.listaUsu));
        this.valid=true;
      }
    },
  }
</script>

