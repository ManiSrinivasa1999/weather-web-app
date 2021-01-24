<template>
  <v-app>
    <v-main>
      <v-container>
        <router-view></router-view>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import { dom } from '@fortawesome/fontawesome-svg-core';

export default {
  name: 'App',
  mounted() {
    dom.watch();
    // console.log(process.env.BASE_URL);
  },
};
</script>
