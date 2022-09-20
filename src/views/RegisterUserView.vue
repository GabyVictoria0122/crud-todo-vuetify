<template>
  <v-container fill-height>
    <v-row class="text-center">
      <v-col md="6" offset-md="3">
        <v-card class="pa-4" outlined tile>
          <h2>Please Sing Up to continue</h2>
          <v-form ref="form" v-model="valid" lazy-validation>
            <v-text-field
              v-model="fullName"
              :rules="fullNameRules"
              label="Full Name"
              required
            ></v-text-field>

            <v-text-field
              v-model="username"
              :rules="usernameRules"
              label="Usuário"
              required
            ></v-text-field>

            <v-text-field
              v-model="email"
              :rules="emailRules"
              label="E-mail"
              required
            ></v-text-field>

            <v-text-field
              v-model="password"
              :append-icon="show1 ? 'mdi-eye' : 'mdi-eye-off'"
              :rules="[passwordRules.required, passwordRules.min]"
              :type="show1 ? 'text' : 'password'"
              name="input-10-1"
              label="Create Password"
              hint="At least 6 characters"
              counter
              @click:append="show1 = !show1"
            ></v-text-field>

            <v-text-field
              v-model="passwordConfirm"
              :append-icon="show2 ? 'mdi-eye' : 'mdi-eye-off'"
              :rules="[passworConfirmRules]"
              :type="show2 ? 'text' : 'password'"
              name="input-10-1"
              label="Confirm Your Password"
              hint="At least 6 characters"
              counter
              @click:append="show2 = !show2"
            ></v-text-field>

            <v-btn
              :loading="loading"
              :disabled="!valid"
              class="mr-4"
              @click="signup"
            >
              Continues
            </v-btn>
          </v-form>
        </v-card>
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
    fullName: '',
    username: '',
    email: '',
    password: '',
    passwordConfirm: '',
    show1: false,
    show2: false,
    fullNameRules: [
      (v) => !!v || 'Name is required',
      (v) =>
        (v && v.length >= 4) || 'The name must be longer than 4 characters',
    ],
    usernameRules: [
      (v) => !!v || 'Username is required',
      (v) =>
        (v && v.length >= 4) || 'The username must be longer than 4 characters',
    ],
    emailRules: [
      (v) => !!v || 'E-mail is required',
      (v) => /.+@.+\..+/.test(v) || 'E-mail must be valid',
    ],
    passwordRules: {
      required: (value) => !!value || 'Required.',
      min: (v) => v.length >= 6 || 'Min 6 characters',
      // emailMatch: () => `The email and password you entered don't match`,
    },
  }),

  methods: {
    signup() {
      AuthApi.signup(this.fullName, this.username, this.email, this.password)
        .then((data) => {
          console.log('data', data)
          this.$router.push({ name: 'login' })
        })
        .catch((error) => {
          console.log('chegou um erro aqui gente:', error)
        })
    },
    passworConfirmRules() {
      if (this.password != this.passwordConfirm) {
        return 'Passwords must be the same'
      }
      return true
    },
  },
}
</script>
