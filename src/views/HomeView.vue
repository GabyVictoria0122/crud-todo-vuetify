<template>
  <v-container>
    <v-row class="text-center ma-16">
      <v-col class="pt-16" cols="12">
        <v-img
          :src="require('../assets/logoTodo.png')"
          class="my-3"
          contain
          height="200"
        />
      </v-col>

      <v-col class="mb-4">
        <h1 class="display-2 font-weight-bold mb-3">
          Bem-vindo ao TODO Vuetify
        </h1>

        <p class="subheading font-weight-regular">
          Gerenciando tarefas aprendendo VueJS + Vuetify + API Mock
        </p>
        <p>
          <v-btn
            class="ma-5"
            x-large
            rounded
            color="light-blue "
            dark
            :to="{ name: 'login' }"
          >
            Iniciar
          </v-btn>
        </p>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {}
</script>
