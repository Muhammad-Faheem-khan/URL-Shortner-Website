<template>
  <v-app>
    <v-app-bar
    class="navbar d-flex align-center"
    app
      dark
    >
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.png"
          transition="scale-transition"
          width="40"
        />

        <h3>URL Shortner</h3>
      </div>

      <v-spacer></v-spacer>

      
    </v-app-bar>

    <v-main class="bg-color">
      <InputSection />
      <DesignComponent />

    </v-main>
  </v-app>
</template>

<script>
import InputSection from './components/InputSection.vue';
import DesignComponent from './components/DesignComponent.vue';
export default {
  name: 'App',

  components: {
    InputSection,
    DesignComponent,
  },

  data: () => ({
    //
  }),
};
</script>
<style scoped>
.navbar{
  background-color: #343a40;
}
.bg-color{
  
  background-color: #fff;
}
</style>