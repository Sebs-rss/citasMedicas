<template>
    <div :style="{ backgroundColor: severityColor }" class="card">
      <h3>{{ appointment.patient }}</h3>
      <p>{{ appointment.date }} - {{ appointment.time }}</p>
      <p>Gravedad: {{ appointment.severity }}</p>
      <p>Motivo: {{ appointment.reason }}</p>
      <button @click="$emit('delete-appointment', appointment)">Eliminar</button>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      appointment: Object
    },
    computed: {
      severityColor() {
        const colors = {
          Baja: 'green',
          Media: 'yellow',
          Alta: 'red'
        };
        return colors[this.appointment.severity] || 'white';
      }
    }
  };
  </script>
  
  <style scoped>
  .card {
    border: 1px solid #ccc;
    padding: 1rem;
    margin: 1rem 0;
  }
  </style>
  