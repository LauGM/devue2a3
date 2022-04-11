<template>
  <v-app>
    <v-main>
        <v-container class="accent">
        <h1>Formulario y tabla con Vue3, Vuetify3</h1>
        <formu-datos />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import FormuDatos from './components/FormuDatos.vue'

export default {
  name: 'App',

  components: {
    FormuDatos,
  },
}
</script>
