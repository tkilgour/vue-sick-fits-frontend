<template>
  <div v-if="error && error.message">
    <div v-if="error.networkError && error.networkError.result && error.networkError.result.errors.length">
      <div v-for="(error, i) in error.networkError.result.errors" :key="i" class="error-styles">
        <p data-test="graphql-error">
          <strong>Shoot!</strong>
          {{error.message.replace('GraphQL error: ', '')}}
        </p>
      </div>
    </div>
    <div v-else class="error-styles">
      <p data-test="graphql-error">
        <strong>Shoot!</strong>
        {{error.message.replace('GraphQL error: ', '')}}
      </p>
    </div>
  </div>  
</template>

<script>
export default {
  name: "DisplayError",
  props: {
    error: Object,
    default: {}
  }
}
</script>

<style lang="scss" scoped>
@import '@/assets/scss/_vars.scss';
  .error-styles {
    padding: 2rem;
    background: white;
    margin: 2rem 0;
    border: 1px solid rgba(0, 0, 0, 0.05);
    border-left: 5px solid red;
    p {
      margin: 0;
      font-weight: 100;
    }
    strong {
      margin-right: 1rem;
    }
  }
</style>
