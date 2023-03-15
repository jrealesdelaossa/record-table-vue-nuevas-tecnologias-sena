<template>
  <div id="app" class="container">
    <h1 class="mb-5">Tabla de Registros</h1>

    <div class="mb-5">
      <formulario-registro @datos-enviados="recibirDatos"/>
    </div>

    <records-table :personaParaGuardar="this.personaParaGuardar"/>
  </div>
</template>

<script>

import FormularioRegistro from "@/components/formularioRegistro.vue";
import RecordsTable from "@/components/recordsTable.vue";

export default {
  name: 'App',
  components: {
    RecordsTable,
    FormularioRegistro
  },

  data () {
    return {
      personaParaGuardar: {},
    }
  },

  methods: {
    recibirDatos(persona) {
      this.personaParaGuardar = persona;
      console.log(JSON.stringify(persona))
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
