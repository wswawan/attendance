<template>
  <v-row justify="center" align="center">
    <v-col cols="12" md="6" sm="8">
      <v-card>
        <v-toolbar>
          <v-icon>mdi-account</v-icon>
          <v-toolbar-title>Login Form</v-toolbar-title>
        </v-toolbar>
        <v-form ref="form" v-model="valid" lazy-validation>
          <v-card-text>
            <v-text-field
              v-model="email"
              append-icon="mdi-at"
              :rules="emailRules"
              label="E-mail"
              type="email"
              required
            ></v-text-field>
          </v-card-text>

          <v-card-text>
            <v-text-field
              v-model="password"
              :append-icon="show ? 'mdi-eye' : 'mdi-eye-off'"
              :password="password"
              :rules="passwordRules"
              :type="show ? 'text' : 'password'"
              required
              label="Password"
              @click:append="show = !show"
            ></v-text-field>
          </v-card-text>
          <v-divider></v-divider>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn
              :disabled="!valid"
              color="success"
              class="mr-4"
              @click="validate"
            >
              Submit
            </v-btn>
          </v-card-actions>
        </v-form>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
export default {
  data: () => ({
    valid: true,
    show: false,
    email: '',
    emailRules: [
      (v) => !!v || 'E-mail is required',
      (v) => /.+@.+\..+/.test(v) || 'E-mail must be valid',
    ],
    passwordRules: [
      (v) => !!v || 'Password is required',
      (v) =>
        (v && v.length > 5) || 'Password must be greater than 6 characters',
    ],
    checkbox: false,
  }),

  methods: {
    validate() {
      this.$refs.form.validate()
    },
    reset() {
      this.$refs.form.reset()
    },
    resetValidation() {
      this.$refs.form.resetValidation()
    },
  },
}
</script>
