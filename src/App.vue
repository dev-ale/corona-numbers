<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
      </div>

      <v-spacer></v-spacer>

      <v-btn
        href="https://github.com/vuetifyjs/vuetify/releases/latest"
        target="_blank"
        text
      >
        <span class="mr-2">info</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main>
      <Numbers/>
    </v-main>
  </v-app>
</template>

<script>
import Numbers from './components/Numbers';
export default {
  name: 'App',

  components: {
    Numbers,
  },

  data(){
    return{

    }
  }
}
</script>
