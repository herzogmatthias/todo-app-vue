<template>
  <v-app>
    <router-view></router-view>
  </v-app>
</template>

<script lang="ts">

import Home from './views/Home.vue';
import { Component, Vue } from 'vue-property-decorator';

@Component({
  components: {
    Home,
},
})
export default class App extends Vue {
}
</script>
