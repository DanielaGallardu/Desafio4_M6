<script>
export default {
  name: 'FormCitas',
  data() {
    return {
      paciente: '',
      fecha: '',
      hora: '',
      gravedad: '',
      motivo: '',
      camposVacios: {
        paciente: false,
        fecha: false,
        hora: false,
        gravedad: false,
        motivo: false,
      },
    };
  },
  computed: {
    formularioCompleto() {
      return this.paciente && this.fecha && this.hora && this.gravedad && this.motivo;
    },
  },
  methods: {
    verificarCampos() {
      this.camposVacios.paciente = !this.paciente;
      this.camposVacios.fecha = !this.fecha;
      this.camposVacios.hora = !this.hora;
      this.camposVacios.gravedad = !this.gravedad;
      this.camposVacios.motivo = !this.motivo;
    },
    enviarCita() {
      const nuevaCita = {
        paciente: this.paciente,
        fecha: this.fecha,
        hora: this.hora,
        gravedad: this.gravedad,
        motivo: this.motivo,
      };
      this.$emit('nueva-cita', nuevaCita);
      this.limpiarFormulario();
    },
    limpiarFormulario() {
      this.paciente = '';
      this.fecha = '';
      this.hora = '';
      this.gravedad = '';
      this.motivo = '';
      this.verificarCampos();
    },
  },
};
</script>

<template>
  <form @submit.prevent="enviarCita" class="formulario-cita">
    <div class="campos-container">
      <div class="campo">
        <label :style="{ color: camposVacios.paciente ? 'red' : 'black' }">Paciente:</label>
        <input type="text" v-model="paciente" @input="verificarCampos" />
      </div>
      <div class="campo">
        <label :style="{ color: camposVacios.fecha ? 'red' : 'black' }">Fecha:</label>
        <input type="date" v-model="fecha" @input="verificarCampos" />
      </div>
      <div class="campo">
        <label :style="{ color: camposVacios.hora ? 'red' : 'black' }">Hora:</label>
        <input type="time" v-model="hora" @input="verificarCampos" />
      </div>
      <div class="campo">
        <label :style="{ color: camposVacios.gravedad ? 'red' : 'black' }">Gravedad:</label>
        <select v-model="gravedad" @input="verificarCampos">
          <option disabled value="">Seleccione...</option>
          <option value="baja">Baja</option>
          <option value="media">Media</option>
          <option value="alta">Alta</option>
        </select>
      </div>
      <div class="campo">
        <label :style="{ color: camposVacios.motivo ? 'red' : 'black' }">Motivo:</label>
        <input type="text" v-model="motivo" @input="verificarCampos" />
      </div>
    </div>

    <!-- Contenedor centrado para el botón Agregar -->
    <div class="btn-container">
      <button type="submit" :disabled="!formularioCompleto" class="btn-agregar">Agregar</button>
    </div>
  </form>
</template>

<style scoped>
/* Contenedor principal del formulario */
.formulario-cita {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 15px;
}

/* Contenedor para alinear los campos horizontalmente */
.campos-container {
  display: flex;
  gap: 15px;
}

/* Estilos para cada campo */
.campo {
  display: flex;
  flex-direction: column;
  text-align: left;
}

input,
select {
  padding: 8px;
  border-radius: 4px;
  border: 1px solid #ccc;
  font-size: 1em;
}

/* Contenedor para centrar el botón */
.btn-container {
  display: flex;
  justify-content: center;
  margin-top: 15px;
}

.btn-agregar {
  padding: 10px;
  background-color: #e7ece7;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.btn-agregar:disabled {
  background-color: #ccc;
  cursor: not-allowed;
}
</style>
