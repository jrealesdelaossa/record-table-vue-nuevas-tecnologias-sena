<template>
  <div class="formulario">

    <form class="row g-3 px-4 form-register">
      <div class="col-md-6">
        <label for="firstName" class="form-label">Nombres</label>
        <input type="text" class="form-control" id="firstName" autocomplete="off" v-model="infoPeople.firstName" required>
      </div>
      <div class="col-md-6">
        <label for="lastName" class="form-label">Apellidos</label>
        <input type="text" class="form-control" id="lastName" autocomplete="off" v-model="infoPeople.lastName">
      </div>
      <div class="col-12">
        <label for="address" class="form-label">Dirección</label>
        <input type="text" class="form-control" id="address" autocomplete="off" v-model="infoPeople.address">
      </div>
      <div class="col-md-6">
        <label for="phone" class="form-label">Celular</label>
        <input type="text" class="form-control" id="phone" autocomplete="off" v-model="infoPeople.phone">
      </div>
      <div class="col-md-6">
        <label for="inputState" class="form-label">Sexo</label>
        <select id="inputState" class="form-select" v-model="infoPeople.sex">
          <option selected>- - -</option>
          <option>Masculino</option>
          <option>Femenino</option>
          <option>Prefiero no decir</option>
        </select>
      </div>

      <div class="col-12 my-4">
        <button type="button" class="btn btn-light" v-on:click="enviarDatos"><i class="bi bi-hdd"></i> Registrar</button>
      </div>
    </form>

  </div>
</template>

<script>
export default {
  name: "formularioRegistro",

  data () {
    return {
      infoPeople: {
        firstName: '',
        lastName: '',
        address: '',
        phone: '',
        sex: ''
      },

      allValid: undefined,
    }
  },

  methods: {
    validaCampos() {
      return this.infoPeople.firstName !== '' && this.infoPeople.lastName !== '';
    },

    enviarDatos() {
      this.allValid = this.validaCampos();

      if (this.allValid) {
        this.$emit("datos-enviados", JSON.parse(JSON.stringify(this.infoPeople)));

        this.infoPeople.firstName = '';
        this.infoPeople.lastName = '';
        this.infoPeople.address = '';
        this.infoPeople.phone = '';
        this.infoPeople.sex = '';
      } else {
        console.log("Error");
      }

    }
  }
}
</script>

<style scoped>
.form-register {
  background-color: #4E6E81;
  color: #ffffff;
  border-radius: 8px;
}
</style>