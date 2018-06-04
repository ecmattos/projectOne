<template>
  <q-page class="flex flex-center">
    <!-- content -->
      <q-card inline style="width: 500px">
        <q-card-title>
          Identifique-se
        </q-card-title>

        <q-card-separator />

        <q-card-main>
          <q-field
            icon="mail"
            :error="$v.form.email.$error"
            error-label="Forneça um e-mail válido"
          >
            <q-input
              float-label="E-mail"
              v-model="form.email"
              @blur="$v.form.email.$touch"
            />
          </q-field>
          <br>
          <q-field
            icon="lock"
            :error="$v.form.password.$error"
            error-label="Obrigatório"
          >
            <q-input
              float-label="Senha"
              type="password"
              v-model="form.password"
              @blur="$v.form.password.$touch"
              @keyup.enter="submit"
            />
          </q-field>
        </q-card-main>

        <q-card-separator />

        <q-card-actions>
          <q-btn color="primary" @click="submit">Submit</q-btn>
        </q-card-actions>

        <q-inner-loading :visible="visible">
          <q-spinner-gears size="50px" color="primary"></q-spinner-gears>
        </q-inner-loading>
      </q-card>
    </q-page>
</template>

<script>
import { required, email } from 'vuelidate/lib/validators'

export default {
  data () {
    return {
      form: {
        email: '',
        password: ''
      }
    }
  },
  validations: {
    form: {
      email: {
        required,
        email
      },
      password: {
        required
      }
    }
  },
  methods: {
    submit () {
      this.$v.form.$touch()
      if (this.$v.form.$error) {
        this.$q.notify('Por favor, verifique os campos.')
      }
    }
  }
}
</script>
