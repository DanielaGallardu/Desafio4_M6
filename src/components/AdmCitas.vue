<script>
import FormCitas from './FormCitas.vue';
import CardCitas from './CardCitas.vue';

export default {
  name: 'AdmCitas',
  components: {
    FormCitas,
    CardCitas,
  },
  data() {
    return {
      citas: [],
    };
  },
  methods: {
    agregarCita(cita) {
      this.citas.push(cita);
    },
    eliminarCita(index) {
      this.citas.splice(index, 1);
    },
  },
};
</script>

<template>
  <div class="app-container">
    <h1>Administrador de Citas Médicas</h1>
    <FormCitas @nueva-cita="agregarCita" />
    <div v-if="citas.length === 0">
      <p>No hay citas registradas.</p>
    </div>
    <div v-else class="citas-container">
      <CardCitas v-for="(cita, index) in citas" :key="index" :cita="cita" @eliminar-cita="eliminarCita(index)" />
    </div>
  </div>
</template>

<style scoped>
.citas-container {
  margin-top: 2.5rem;
  display: flex;
  flex-wrap: wrap;
  gap: 2rem;

  justify-content: center;

}
</style>
