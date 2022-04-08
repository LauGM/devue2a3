<template>
    <v-container>
        <h4>Lista de usuarios</h4>
        <v-table>
          <thead>
            <tr>
              <th>
                Nombre
              </th>
              <th>
                Celular
              </th>
              <th>
                Email
              </th>
              <th>
                Suscripto
              </th>
            </tr>
          </thead>
          <tbody>
            <tr
              v-for="item in lista"
              :key="item.name"
            >
              <td>{{ item.nombre }}</td>
              <td>{{ item.celular }}</td>
              <td>{{ item.email }}</td>
              <td>{{ item.suscripto }}</td>
            </tr>
          </tbody>
        </v-table>
    </v-container>
</template>

<script>
  export default {
    data () {
      return {
        }
        
    },
    props:{
        lista: Array
    },
    methods: {
      }
  }
</script>