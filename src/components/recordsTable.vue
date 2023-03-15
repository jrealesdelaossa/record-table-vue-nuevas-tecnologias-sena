<template>
  <div class="record-table">
    <table class="table">
      <thead>
      <tr>
        <th scope="col">#</th>
        <th scope="col">Nombres</th>
        <th scope="col">Apellidos</th>
        <th scope="col">Celular</th>
        <th scope="col">Sexo</th>
        <th scope="col">Dirección</th>
      </tr>
      </thead>
      <tbody class="table-group-divider">
      <tr v-bind:key="people.firstName" v-for="(people, index) in personas">
        <th scope="row">{{ index + 1 }}</th>
        <td>{{ people.firstName }}</td>
        <td>{{ people.lastName }}</td>
        <td>{{ people.phone }}</td>
        <td>{{ people.sex }}</td>
        <td>{{ people.address }}</td>
        <td>
          <button type="button" class="btn btn-outline-info" data-bs-toggle="modal" data-bs-target="#exampleModal" @click="editPeople(index)">
            <i class="bi bi-pencil-square"></i> Editar
          </button>
        </td>

        <td>
          <button type="button" class="btn btn-danger" @click="deletePeople(index)">
            <i class="bi bi-trash"></i> Eliminar
          </button>
        </td>
        </tr>
      </tbody>
    </table>

    <!-- Modal -->
    <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h1 class="modal-title fs-5" id="exampleModalLabel">Datos a editar</h1>
            <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
          </div>
          <div class="modal-body">
            <form class="row g-3">
              <div class="col-md-12">
                <label for="firstName" class="form-label text-start">Nombres</label>
                <input type="text" class="form-control" id="firstName" autocomplete="off" v-model="personaParaEditar.firstName">
              </div>

              <div class="col-md-12">
                <label for="lastName" class="form-label text-start">Apellidos</label>
                <input type="text" class="form-control" id="lastName" autocomplete="off" v-model="personaParaEditar.lastName">
              </div>

              <div class="col-md-12">
                <label for="address" class="form-label text-start">Dirección</label>
                <input type="text" class="form-control" id="address" autocomplete="off" v-model="personaParaEditar.address">
              </div>

              <div class="col-md-12">
                <label for="phone" class="form-label text-start">Celular</label>
                <input type="text" class="form-control" id="phone" autocomplete="off" v-model="personaParaEditar.phone">
              </div>

              <div class="col-md-12">
                <label for="sex" class="form-label">Sexo</label>
                <select id="sex" class="form-select" v-model="personaParaEditar.sex">
                  <option selected>- - -</option>
                  <option>Masculino</option>
                  <option>Femenino</option>
                  <option>Prefiero no decir</option>
                </select>
              </div>
            </form>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Cerrar</button>
            <button type="button" class="btn btn-success" data-bs-dismiss="modal" @click="saveChanges">Guardar Cambios</button>
          </div>
        </div>
      </div>
    </div>
  </div>


</template>

<script>
export default {
  name: "recordsTable",

  props: {
    personaParaGuardar: {}
  },

  watch: {
    personaParaGuardar(nuevoValor, antiguoValor) {
      console.log(`El valor de miAtributo ha cambiado de ${antiguoValor.firstName} a ${nuevoValor.firstName}`);
      this.agregarPersona(JSON.parse(JSON.stringify(nuevoValor)));
    }
  },

  data () {
    return {
      personas: [],
      indexOfPeopleByEdit: '',

      personaParaEditar: {

      }
    }
  },

  methods: {
    agregarPersona(persona) {
      this.personas.push(persona);
    },

    editPeople (indexPeople) {
      this.personaParaEditar = JSON.parse(JSON.stringify(this.personas[indexPeople]));
      this.indexOfPeopleByEdit = indexPeople;
    },

    saveChanges () {
      this.personas[this.indexOfPeopleByEdit] = this.personaParaEditar;

      this.indexOfPeopleByEdit = '';
      this.personaParaEditar = {};
      this.$forceUpdate();
    },

    deletePeople (indexPeople) {
      this.personas.splice(indexPeople, 1);
      this.$forceUpdate();
    }
  }
}
</script>

<style scoped>

</style>