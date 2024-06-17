<template>
  <div id="app">
    <h1>Administrador de Citas Médicas</h1>
    <form @submit.prevent="agregarCita">
      <div>
        <label :style="{ color: paciente ? 'black' : 'red' }">Paciente</label>
        <input v-model="paciente" type="text" />
      </div>
      <div>
        <label :style="{ color: fecha ? 'black' : 'red' }">Fecha</label>
        <input v-model="fecha" type="date" />
      </div>
      <div>
        <label :style="{ color: hora ? 'black' : 'red' }">Hora</label>
        <input v-model="hora" type="time" />
      </div>
      <div>
        <label :style="{ color: gravedad ? 'black' : 'red' }">Gravedad</label>
        <select v-model="gravedad">
          <option value="">Seleccionar</option>
          <option value="Baja">Baja</option>
          <option value="Media">Media</option>
          <option value="Alta">Alta</option>
        </select>
      </div>
      <div>
        <label :style="{ color: motivo ? 'black' : 'red' }">Motivo</label>
        <input v-model="motivo" type="text" />
      </div>
      <button type="submit" :disabled="!formularioCompleto">Agregar</button>
    </form>
    <div v-if="citas.length === 0">
      <p>No hay citas registradas aún.</p>
    </div>
    <CitaCard
      v-else
      v-for="cita in citas"
      :key="cita.fecha + cita.hora"
      :cita="cita"
      @eliminar="eliminarCita"
    />
  </div>
</template>

<script>
import CitaCard from './components/CitaCard.vue';

export default {
  name: 'App',
  components: {
    CitaCard,
  },
  data() {
    return {
      paciente: '',
      fecha: '',
      hora: '',
      gravedad: '',
      motivo: '',
      citas: [],
    };
  },
  computed: {
    formularioCompleto() {
      return (
        this.paciente &&
        this.fecha &&
        this.hora &&
        this.gravedad &&
        this.motivo
      );
    },
  },
  methods: {
    agregarCita() {
      const nuevaCita = {
        paciente: this.paciente,
        fecha: this.fecha,
        hora: this.hora,
        gravedad: this.gravedad,
        motivo: this.motivo,
      };
      this.citas.push(nuevaCita);
      this.reiniciarFormulario();
    },
    reiniciarFormulario() {
      this.paciente = '';
      this.fecha = '';
      this.hora = '';
      this.gravedad = '';
      this.motivo = '';
    },
    eliminarCita(cita) {
      this.citas = this.citas.filter(
        (c) => c.fecha !== cita.fecha || c.hora !== cita.hora
      );
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
}

form {
  display: grid;
  grid-template-columns: 1fr 2fr;
  grid-gap: 10px;
  margin-bottom: 20px;
}

label {
  text-align: right;
}

button {
  grid-column: 1 / -1;
  margin-top: 10px;
}
</style>