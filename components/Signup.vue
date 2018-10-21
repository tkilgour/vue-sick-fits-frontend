<template>
  <ApolloMutation 
    :mutation="require('@/apollo/mutations/signup.gql')"
    :variables="state"
    @done="state = { name: '', email: '', password: '' }"
  >
    <template slot-scope="{mutate, loading, error}">
      <form method="post" @submit.prevent="mutate">
        <fieldset :disabled="loading" :aria-busy="loading">
          <h2>Sign Up for An Account</h2>
          <Error :error="error"></Error>
          <label for="email">
            Email
            <input
              type="email"
              name="email"
              placeholder="email"
              v-model="state.email"
            />
          </label>
          <label for="name">
            Name
            <input
              type="text"
              name="name"
              placeholder="name"
              v-model="state.name"
            />
          </label>
          <label for="password">
            Password
            <input
              type="password"
              name="password"
              placeholder="password"
              v-model="state.password"
            />
          </label>
          <button type="submit">Sign Up!</button>
        </fieldset>
      </form>
    </template>
  </ApolloMutation>
</template>

<script>
import Error from "./ErrorMessage";

export default {
  name: "Signup",
  components: {
    Error
  },
  data() {
    return {
      state: {
        email: '',
        name: '',
        password: ''
      }
    }
  },
  methods: {
  }
}
</script>

<style lang="scss" scoped>
@import '@/assets/scss/_form.scss';
</style>