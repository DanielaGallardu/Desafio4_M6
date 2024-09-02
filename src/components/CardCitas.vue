<script>
export default {
  name: 'CardCitas',
  props: {
    cita: {
      type: Object,
      required: true,
    },
  },
  computed: {
    // Determina la clase de color según la gravedad de la cita
    claseGravedad() {
      switch (this.cita.gravedad) {
        case 'alta':
          return 'red';
        case 'media':
          return 'yellow';
        case 'baja':
          return 'green';
        default:
          return '';
      }
    },
  },
};
</script>

<template>
  <div :class="['cita-card', claseGravedad]">
    <h2 class="tittle-card">Paciente</h2>
    <h2 class="paciente">{{ cita.paciente }}</h2>
    <p>Fecha: {{ cita.fecha }}</p>
    <p>Hora: {{ cita.hora }}</p>
    <p>Motivo: {{ cita.motivo }}</p>
    <button @click="$emit('eliminar-cita')">Eliminar</button>
  </div>
</template>

<style scoped>
.cita-card {
  display: flex;
  flex-direction: column;
  min-width: 10rem;
  padding: 20px;
  margin: 10px 0;
  border-radius: 5px;
  color: white;
  text-align: left;
}


.yellow {
  background-color: #eaec45;
}

.green {
  background-color: rgb(171, 226, 140);
}

.red {
  background-color: rgb(243, 110, 110);
}
</style>
