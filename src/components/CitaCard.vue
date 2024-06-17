<template>
  <div
    class="cita-card"
    :style="{ backgroundColor: getBackgroundColor(cita.gravedad) }"
  >
    <h3>{{ cita.paciente }}</h3>
    <p>Fecha: {{ cita.fecha }}</p>
    <p>Hora: {{ cita.hora }}</p>
    <p>Gravedad: {{ cita.gravedad }}</p>
    <p>Motivo: {{ cita.motivo }}</p>
    <button @click="eliminarCita">Eliminar</button>
  </div>
</template>

<script>
export default {
  name: 'CitaCard',
  props: {
    cita: {
      type: Object,
      required: true,
    },
  },
  methods: {
    eliminarCita() {
      this.$emit('eliminar', this.cita);
    },
    getBackgroundColor(gravedad) {
      switch (gravedad) {
        case 'Baja':
          return 'green';
        case 'Media':
          return 'yellow';
        case 'Alta':
          return 'red';
        default:
          return '#ccc';
      }
    },
  },
};
</script>

<style scoped>
.cita-card {
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  margin-bottom: 20px;
}
</style>