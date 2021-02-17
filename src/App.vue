<template>
  <v-app>
    <v-app-bar
      app
      color="#f2f2f2"
      dark
    >
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="./assets/logo.png"
          transition="scale-transition"
          width="40"
        />
      </div>
      <v-spacer></v-spacer>
    </v-app-bar>
    <v-main>
      <Upload/>
    </v-main>
  </v-app>
</template>

<script>
import Upload from './components/Upload';

export default {
  name: 'App',

  components: {
    Upload,
  },

  data: () => ({
    //
  }),
};
</script>
