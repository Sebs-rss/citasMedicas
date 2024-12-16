<script>
import { ref } from 'vue';
import AppointmentForm from './components/AppointmentForm.vue';
import AppointmentCard from './components/AppointmentCard.vue';

export default {
  components: {
    AppointmentForm,
    AppointmentCard
  },
  setup() {
    const appointments = ref([]);

    const addAppointment = (appointment) => {
      appointments.value.push({ ...appointment, id: Date.now() });
    };

    const deleteAppointment = (appointment) => {
      appointments.value = appointments.value.filter(a => a.id !== appointment.id);
    };

    return {
      appointments,
      addAppointment,
      deleteAppointment
    };
  }
};
</script>

<template>
  <div id="app">
    <AppointmentForm @add-appointment="addAppointment" />
    <div v-if="appointments.length === 0">
      <p>No hay consultas registradas</p>
    </div>
    <div v-else>
      <AppointmentCard
        v-for="appointment in appointments"
        :key="appointment.id"
        :appointment="appointment"
        @delete-appointment="deleteAppointment"
      />
    </div>
  </div>
</template>


<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
