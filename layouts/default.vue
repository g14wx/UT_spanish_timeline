<template>
  <v-app dark>
    <v-app-bar
      :clipped-left="true"
      fixed
      app
    >
      <v-toolbar-title v-text="title" />
      <v-spacer />
    </v-app-bar>
    <v-main>
      <v-container>
        <nuxt />
      </v-container>
    </v-main>
    <v-footer
      :absolute="true"
      app
    >
      <span>&copy; {{ new Date().getFullYear() }} Carlos Jose Hernandez Dueñas</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data () {
    return {
      title: 'Tarea #1 Desarrollo de la lectura y composición'
    }
  }
}
</script>
