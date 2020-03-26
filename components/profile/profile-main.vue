<template>
  <div>
    <v-card
      class="mx-auto"
      max-width="344"
      outlined
    >
      <form
        @submit.prevent="submit"
        class="mx-5"
      >
        <v-text-field
          label="Имя"
          v-model="name"
          :error-messages="nameErrors"
          required
          @blur="$v.name.$touch()"
        ></v-text-field>
        <v-text-field
          label="Фамилия"
          v-model="surename"
          :error-messages="surenameErrors"
          required
          @blur="$v.surename.$touch()"
        ></v-text-field>
        <v-text-field
          v-model="email"
          :error-messages="emailErrors"
          label="E-mail"
          required
          @blur="$v.email.$touch()"
        ></v-text-field>
        <v-text-field
          label="Профиль в vk"
          v-model="vkProfile"
          :error-messages="vkProfileErrors"
          required
          :disabled = "true"
          @blur="$v.vkProfile.$touch()"
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
      </form>
    </v-card>
  </div>
</template>

<script>
import { validationMixin } from 'vuelidate'
  import { required, minLength, maxLength, sameAs, email} from 'vuelidate/lib/validators'
  export default {
    data: () => ({
      name: '',
      surename: '',
      email: '',
      vkProfile: '',
      password: '',
      confirm: ''
    }),
    mixins: [validationMixin],
    head: {
      title: 'Вход'
    },
    validations: {
      name: { required, maxLength: maxLength(10) },
      surename: { required, maxLength: maxLength(20) },
      vkProfile: { required, maxLength: maxLength(30) },
      email: { required, email },
      password: { required, minLength:  minLength(6) },
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
      surenameErrors () {
        const errors = []
        if (!this.$v.surename.$dirty) return errors
        !this.$v.surename.maxLength && errors.push('Длина имени не более 20 символов')
        !this.$v.surename.required && errors.push('Имя не должно быть пустым')
        return errors
      },
      vkProfileErrors () {
        const errors = []
        if (!this.$v.vkProfile.$dirty) return errors
        !this.$v.vkProfile.maxLength && errors.push('Длина имени не более 30 символов')
        !this.$v.vkProfile.required && errors.push('Имя не должно быть пустым')
        return errors
      },
      emailErrors () {
        const errors = []
        if (!this.$v.email.$dirty) return errors
        !this.$v.email.email && errors.push('Введите верный email')
        !this.$v.email.required && errors.push('Заполните E-mail')
        return errors
      },
       passwordErrors () {
        const errors = []
        if (!this.$v.password.$dirty) return errors
        !this.$v.password.required && errors.push('Пароль не может быть пустым')
        !this.$v.password.minLength && errors.push('Длина пароля не менее 6 символов')
        return errors
      },
      confirmErrors () {
        const errors = []
        if (!this.$v.confirm.$dirty) return errors
        !this.$v.confirm.sameAs && errors.push('Пароли не совпадают')
        return errors
      }
    }
  }
</script>

<style scoped>

</style>
