<template>
  <v-container>
    <!-- snackbar -->
    <v-snackbar v-model="snackbar.show" :value="true" absolute left shaped top>
      {{ snackbar.message }}
    </v-snackbar>
    <v-row class="text-center pa-16 ma-16">
      <v-col md="6" offset-md="3">
        <v-card class="pa-4 rounded mt-6" outlined tile>
          <h2>Login</h2>
          <v-form ref="form" v-model="valid" lazy-validation>
            <v-text-field
              v-model="username"
              label="Username"
              required
              outlined
              append-icon="fa-user"
              :rules="usernameRules"
              v-on:keyup.enter="login"
            ></v-text-field>

            <v-text-field
              v-model="password"
              :append-icon="show1 ? 'mdi-eye' : 'mdi-eye-off'"
              :rules="[rules.required, rules.min]"
              :type="show1 ? 'text' : 'password'"
              name="input-10-1"
              label="Password"
              counter
              outlined
              @click:append="show1 = !show1"
              v-on:keyup.enter="login"
            ></v-text-field>

            <v-row class="d-flex justify-space-around">
              <v-checkbox
                v-model="checkbox"
                label="Remember me"
                required
              ></v-checkbox>

              <p class="ma-4">
                <span class="subtitle-1">
                  <a href="">Forget your password?</a></span
                >
              </p>
            </v-row>

            <v-btn
              :loading="loading"
              :disabled="!valid"
              class="mr-4"
              @click="login"
            >
              Let me in!
            </v-btn>
          </v-form>
        </v-card>
        <p class="ma-4">
          <span class="subtitle-1">
            New User?
            <router-link :to="{ name: 'registro' }">SingUp</router-link>
          </span>
        </p>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import AuthApi from '@/api/auth.api.js'

export default {
  data: () => ({
    loading: false,
    valid: true,
    name: '',
    show1: false,
    password: '',
    snackbar: {
      show: false,
      message: '',
    },
    rules: {
      required: (value) => !!value || 'Required.',
      min: (v) => v.length >= 6 || 'Min 6 characters',
      emailMatch: () => `The email and password you entered don't match`,
    },
    username: '',
    usernameRules: [
      (v) => !!v || 'Username is required',
      (v) =>
        (v && v.length >= 4) || 'The username must be longer than 4 characters',
    ],

    checkbox: false,
  }),

  methods: {
    login() {
      this.loading = true
      this.$refs.form.validate()
      AuthApi.login(this.username, this.password)
        .then((user) => {
          console.log('login ok', user)
          this.saveLoggedUser(user)
          this.$router.push({ name: 'taskSummary' })
        })
        .catch((error) => {
          console.log('login falhou', error)
          this.snackbar.message = 'Usuario ou senha invalida'
          this.snackbar.show = true
        })
        .finally(() => {
          this.loading = false
        })
    },
    saveLoggedUser(user) {
      window.localStorage.setItem('loggedUser', user.id)
      window.localStorage.setItem('loggedUserToken', user.token)
    },
  },
}
</script>
