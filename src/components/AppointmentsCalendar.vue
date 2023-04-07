<template>
  <v-container>
    <v-card>
      <FullCalendar :options="calendarOptions" />
    </v-card>
  </v-container>
</template>

<script>
import FullCalendar from '@fullcalendar/vue'
import dayGridPlugin from '@fullcalendar/daygrid'
import axios from 'axios'

export default {
  components: {
    FullCalendar
  },
  data() {
    return {
      calendarOptions: {
        plugins: [dayGridPlugin],
        initialView: 'dayGridMonth',
        events: [
        ],
        datesSet: this.handleDatesSet, // asignar callback
      },
      dates: {
        start: 1,
        end: 2
      }
    }
  },
  methods: {
    foo(val) {
      this.dates = val
      console.log(val);
    },
    loadEvents() {
      axios.get('http://localhost:8000/api/appointments', { params: this.dates })
        .then(response => {
          const data = response.data;
          const appointments = data.map((appointment) => ({ title: appointment.patientname, date: appointment.appointment_date_and_time }));
          this.calendarOptions.events = appointments

        })
        .catch(error => {
          console.log(error)
        })
    },
    handleDatesSet(val) {

      this.dates.start = val.startStr
      this.dates.end = val.endStr
      this.loadEvents()
    }
  },
  mounted() {
    this.loadEvents()
  }
}
</script>
