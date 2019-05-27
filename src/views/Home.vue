<template>
<v-app>
  <Navbar></Navbar>
  <v-content>
    <v-form ref="form" v-model="valid" lazy-validation>
    <v-container>
      <v-layout>
        <v-flex
          xs12
          md4
        >
          <v-text-field
            v-model="firstname"
            :rules="nameRules"
            :counter="10"
            label="First name"
            required
          ></v-text-field>
        </v-flex>

        <v-flex
          xs12
          md4
        >
          <v-text-field
            v-model="lastname"
            :rules="nameRules"
            :counter="10"
            label="Last name"
            required
          ></v-text-field>
        </v-flex>

        <v-flex
          xs12
          md4
        >
          <v-text-field
            v-model="email"
            :rules="emailRules"
            label="E-mail"
            required
          ></v-text-field>
        </v-flex>
      </v-layout>
      <v-layout align-center>
        <v-flex
          xs12
          md4
          align-center
        >
          <v-textarea
            v-model="description"
            :rules="descriptionRules"
            label="Description"
            required
          ></v-textarea>
        </v-flex>
        <v-flex
          xs12
          md4
          align-center
        >
          <v-text-field
            v-model="title"
            :rules="titleRules"
            label="Title"
            required
          ></v-text-field>
        </v-flex>
        <v-flex
          xs12
          md4
        >
                <v-menu
        ref="menu"
        v-model="menu"
        :close-on-content-click="false"
        :nudge-right="40"
        :return-value.sync="date"
        lazy
        transition="scale-transition"
        offset-y
        full-width
        min-width="290px"
      >
        <v-text-field
          slot="activator"
          v-model="date"
          label="Date"
          prepend-icon="event"
          readonly
        ></v-text-field>
        <v-date-picker v-model="date" no-title scrollable>
          <v-spacer></v-spacer>
          <v-btn flat color="primary" @click="menu = false">Cancel</v-btn>
          <v-btn flat color="primary" @click="$refs.menu.save(date)">OK</v-btn>
        </v-date-picker>
      </v-menu>
        </v-flex>
      </v-layout>
    </v-container>
    <v-layout justify-end>
      <v-btn :right="true"
      :disabled="!valid"
      color="success"
      @click="submit"
    >Submit</v-btn>
    </v-layout>
  </v-form>
  <v-layout>
    <v-container>
          <v-list two-line>
          <template v-for="(item, index) in appointmentList">
            <v-list-tile
              :key="index"
              avatar
            >
              <ListItem :appointment=item @delete="del"></ListItem>
              
            </v-list-tile>
          </template>
        </v-list>
    </v-container>

  </v-layout>
  </v-content>
</v-app>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import Navbar from '@/components/Navbar.vue';
import ListItem from '@/components/ListItem.vue';
import {Appointment} from '../models/appointment';


@Component({
  components: {
    Navbar,
    ListItem,
  },
  computed: {
  form(): any {
    return this.$refs.form as any;
  },
},
})
export default class Home extends Vue {
  private valid: boolean = false;
  private appointmentList: Appointment[] = [];
  private form!: any;
  private menu = false;
  private firstname: string = '';
  private id: number = 0;
  private title: string = '';
  private lastname: string = '';
  private email: string = '';
  private description: string = '';
  private date = new Date().toISOString().substr(0, 10);
  private descriptionRules = [
    (v: string) => !!v || 'Description is required',
  ];
  private titleRules = [
    (v: string) => !!v || 'Title is required',
  ];
  private nameRules = [
        (v: string) => !!v || 'Name is required',
        (v: string) => v.length <= 10 || 'Name must be less than 10 characters',
      ];
  private emailRules = [
        (v: string) => !!v || 'E-mail is required',
        (v: string) => /.+@.+/.test(v) || 'E-mail must be valid',
      ];
  private mounted() {
    if (!!Vue.prototype.$appointmentList) {
      this.appointmentList = Vue.prototype.$appointmentList;
    }
  }
  private del(id: string) {
    this.appointmentList.splice(this.appointmentList.findIndex((appointment) => appointment.id as string === id));
    Vue.prototype.$appointmentList = this.appointmentList;
  }
  private submit() {
    if (this.form.validate()) {
      this.valid = true;
      this.appointmentList.push({
        firstname: this.firstname,
        lastname: this.lastname,
        date: this.date,
        description: this.description,
        email: this.email,
        title: this.title,
        id: this.ID(),
      });
      Vue.prototype.$appointmentList = this.appointmentList;
    } else {
      this.valid = false;
    }
  }
  private ID = () => {
  return '_' + Math.random().toString(36).substr(2, 9);
}
}
</script>


