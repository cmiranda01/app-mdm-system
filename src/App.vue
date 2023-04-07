<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
       mdm-system
      </div>

      <v-spacer></v-spacer>

     
    </v-app-bar>

    <v-main>
      <AppointmentsCalendar />

    </v-main>
  </v-app>
</template>

<script>
import AppointmentsCalendar from '@/components/AppointmentsCalendar.vue'

export default {
  name: 'App',

  components: {
    AppointmentsCalendar
  },
 


};
</script>

<style>
.app-container {
  padding: 20px;
}
</style>
