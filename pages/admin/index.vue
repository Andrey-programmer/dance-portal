<template>
  <v-container>
    <v-row
      class="fullHeight"
      justify="center"
      align="center"
    >
      <v-col
        cols='4'
      >
        <form
          @submit.prevent="submit"
        >
          <v-text-field
            label="Имя"
            v-model="name"
            :error-messages="nameErrors"
            required
            @blur="$v.name.$touch()"
          ></v-text-field>
          <v-text-field
            label="Пароль"
            v-model="password"
            :counter="10"
            :error-messages="passwordErrors"
            required
            @blur="$v.password.$touch()"
          ></v-text-field>
          <v-btn
            class="mr-4"
            @click="clear"
          >
            Очистить форму
          </v-btn>
          <v-btn
            class="mr-4"
            @click="submit"
            :disabled="$v.$invalid"
          >
            Войти
          </v-btn>
        </form>
      </v-col>
    </v-row>
  </v-container>

</template>

<script>
  import { validationMixin } from 'vuelidate'
  import { required, minLength, maxLength } from 'vuelidate/lib/validators'

  export default {
    data: () => ({
      source: '',
      name: '',
      password: ''
    }),
    layout: 'autorization',
    mixins: [validationMixin],
    head: {
      title: 'Админка'
    },
    validations: {
      name: { required, maxLength: maxLength(10) },
      password: { required, minLength: minLength(3) },
    },
    computed: {
      nameErrors () {
        const errors = []
        if (!this.$v.name.$dirty) return errors
        !this.$v.name.maxLength && errors.push('Длина имени не более 10 символов')
        !this.$v.name.required && errors.push('Имя не должно быть пустым')
        return errors
      },
      passwordErrors () {
        const errors = []
        if (!this.$v.password.$dirty) return errors
        !this.$v.password.required && errors.push('Пароль не может быть пустым')
        !this.$v.password.minLength && errors.push('Длина пароля не менее 3 символов')
        return errors
      },
    },
    methods: {
      submit () {
      },
      clear () {
        this.$v.$reset()
        this.name = ''
        this.password = ''
      }
    }
  }
</script>

<style lang="scss" scoped>

</style>
