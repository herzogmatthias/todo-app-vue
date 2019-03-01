<template>
  <v-app>
    <Navbar></Navbar>
    <v-content :v-if="this.selectedAppointment != null">
      <v-layout mt-3 justify-center>
        <h1 class="text-uppercase">{{selectedAppointment.title}}</h1>
      </v-layout>
      <v-divider/>
      <v-layout row wrap align-center justify-space-between>
        <v-flex>
          <div class="d-flex align-center"><v-icon large>account_circle</v-icon><h3>{{selectedAppointment.firstname}} {{selectedAppointment.lastname}}</h3></div>
        </v-flex>
        <v-flex align-center>
          <div class="d-flex align-center"><v-icon large>email</v-icon><h3>{{selectedAppointment.email}}</h3></div>
        </v-flex>
      </v-layout>
      <v-layout justify-space-between mt-5>
        <v-flex align-center>
          <div class="d-flex align-center"><v-icon large>description</v-icon><h3>{{selectedAppointment.description}}</h3></div>
        </v-flex>
        <v-flex align-center>
          <div class="d-flex align-center"><v-icon large>alarm</v-icon><h3>{{selectedAppointment.date}}</h3></div>
        </v-flex>
      </v-layout>
    </v-content>
  </v-app>
</template>
<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import Navbar from '@/components/Navbar.vue';
import { Appointment } from '@/models/appointment';

@Component({
  components: {
    Navbar,
  },
})
export default class ListDetails extends Vue {
  private selectedAppointment: Appointment = {} as Appointment;
  private mounted() {
    this.selectedAppointment = Vue.prototype.$appointmentList.find((appointment: any) => {
      return appointment.id as string === this.$route.params.id;
    });
  }
}
</script>
