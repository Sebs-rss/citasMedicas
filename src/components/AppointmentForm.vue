<template>
    <form @submit.prevent="addAppointment">
      <div v-for="field in fields" :key="field.name" class="form-group">
        <label :style="{ color: isFieldEmpty(field.name) ? 'red' : 'black' }">{{ field.label }}</label>
        <input v-if="field.type === 'text'" :type="field.type" v-model="appointment[field.name]" @input="validateForm" />
        <select v-else-if="field.name === 'severity'" v-model="appointment[field.name]">
          <option value="">Seleccione una opci n</option>
          <option value="Baja">Baja</option>
          <option value="Media">Media</option>
          <option value="Alta">Alta</option>
        </select>
        <input v-else :type="field.type" v-model="appointment[field.name]" @input="validateForm" />
      </div>
      <button type="submit" :disabled="!isFormValid">Agregar</button>
    </form>
  </template>
  
  <script>
  export default {
    data() {
      return {
        appointment: {
          patient: '',
          date: '',
          time: '',
          severity: '',
          reason: ''
        },
        fields: [
          { name: 'patient', label: 'Paciente', type: 'text' },
          { name: 'date', label: 'Fecha', type: 'date' },
          { name: 'time', label: 'Hora', type: 'time' },
          { name: 'severity', label: 'Gravedad', type: 'select' },
          { name: 'reason', label: 'Motivo', type: 'text' }
        ]
      };
    },
    computed: {
      isFormValid() {
        return Object.values(this.appointment).every(value => value);
      }
    },
    methods: {
      isFieldEmpty(field) {
        return !this.appointment[field];
      },
      validateForm() {
        this.isFormValid;
      },
      addAppointment() {
        this.$emit('add-appointment', { ...this.appointment });
        this.resetForm();
      },
      resetForm() {
        this.appointment = {
          patient: '',
          date: '',
          time: '',
          severity: '',
          reason: ''
        };
      }
    }
  };
  </script>
  
  <style scoped>
  .form-group {
    margin-bottom: 1rem;
  }
  </style>
  
