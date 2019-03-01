<template>
<v-layout>
<v-list-tile-content>
        <v-list-tile-title>{{appointment.title}}</v-list-tile-title>
        <v-list-tile-sub-title>{{appointment.email}} - {{appointment.firstname}} {{appointment.lastname}}</v-list-tile-sub-title>
    </v-list-tile-content>
    <v-list-tile-action>
              <v-btn @click="() => redirect(appointment.id)" icon ripple>
                <v-icon color="grey lighten-1">info</v-icon>
              </v-btn>
            </v-list-tile-action>
            <v-list-tile-action>
              <v-btn icon ripple @click="() => del(appointment.id)">
                <v-icon color="grey lighten-1">delete</v-icon>
              </v-btn>
            </v-list-tile-action>
</v-layout>
</template>

<script lang="ts">
import { Component, Vue, Prop, Emit } from 'vue-property-decorator';
import {Appointment} from '../models/appointment';

@Component({})
export default class ListItem extends Vue {
   @Prop() private appointment: any;
    private del(id: string) {
        this.emitDelete(id);
  }
  private redirect(id: string) {
    this.$router.push('/list-details/' + id);
  }
  @Emit('delete') private emitDelete(id: string) {}
}
</script>
