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
            v-model="email"
            :error-messages="emailErrors"
            label="E-mail"
            required
            @blur="$v.email.$touch()"
          ></v-text-field>
          <v-text-field
            label="Пароль"
            v-model="password"
            :counter="16"
            :error-messages="passwordErrors"
            required
            @blur="$v.password.$touch()"
          ></v-text-field>
          <v-text-field
            label="Повторите пароль"
            v-model="confirm"
            :counter="16"
            :error-messages="confirmErrors"
            required
            @blur="$v.confirm.$touch()"
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
          <nuxt-link to="/registration" class="mt-5 d-inline-block">Зарегистрироваться</nuxt-link>
        </form>
      </v-col>
    </v-row>
  </v-container>

</template>

<script>
  import { validationMixin } from 'vuelidate'
  import { required, minLength, maxLength, sameAs, email} from 'vuelidate/lib/validators'

  export default {
    layout: 'autorization',
    data: () => ({
      source: '',
      name: '',
      email: '',
      password: '',
      confirm: ''
    }),
    mixins: [validationMixin],
    head: {
      title: 'Вход'
    },
    validations: {
      name: { required, maxLength: maxLength(10) },
      email: { required, email },
      password: { required, minLength:  minLength(3) },
      confirm: { sameAs: sameAs('password') }
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
      emailErrors () {
        const errors = []
        if (!this.$v.email.$dirty) return errors
        !this.$v.email.email && errors.push('Введите верный email')
        !this.$v.email.required && errors.push('Заполните E-mail')
        return errors
      },
      confirmErrors () {
        const errors = []
        if (!this.$v.confirm.$dirty) return errors
        !this.$v.confirm.sameAs && errors.push('Пароли не совпадают')
        return errors
      }
    },
    methods: {
      submit () {
        this.$v.$touch()
      },
      clear () {
        this.$v.$reset()
        this.name = ''
        this.email = ''
        this.password = ''
        this.confirm = ''
      }
    }
  }
</script>

<style lang="scss" scoped>

</style>
