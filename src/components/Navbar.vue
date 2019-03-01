<template>
    <v-toolbar app>
      <v-toolbar-title class="headline text-uppercase">
        <span>Vue.JS</span>
        <span class="font-weight-light">TODO APP</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn
        flat
        :exact=true
        :to="'/'"
      >
        <span class="mr-2">Home</span>
      </v-btn>
    </v-toolbar>
</template>
<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
@Component
export default class Navbar extends Vue {

}
</script>