<template>
  <ApolloQuery 
    :query="require('@/apollo/queries/singleItem.gql')"
    :variables="{id}"
    @result="({data}) => title = data.item.title"
  >
    <template slot-scope="{ result: { data, error }, isLoading}">
      <Error v-if="error" :error="error" />
      <p v-else-if="isLoading">Loading...</p>
      <div v-else class="single-item-styles">
        <img :src="data.item.largeImage" :alt="data.item.title">
        <div class="details">
          <h2>Viewing {{ data.item.title }}</h2>
          <p>{{ data.item.description }}</p>
        </div>
      </div>
    </template>
  </ApolloQuery>
</template>

<script>
import Error from "./ErrorMessage";

export default {
  name: "SingleItem",
  head() {
    return {
      title: `Sick Fits | ${this.title}`
    }
  },
  props: {
    id: String
  },
  components: {
    Error
  },
  data() {
    return {
      title: '...'
    }
  }
}
</script>

<style lang="scss" scoped>
@import '@/assets/scss/_vars.scss';

.single-item-styles {
  max-width: 1200px;
  margin: 2rem auto;
  box-shadow: $bs;
  display: grid;
  grid-auto-columns: 1fr;
  grid-auto-flow: column;
  min-height: 800px;
  img {
    width: 100%;
    height: 100%;
    object-fit: contain;
  }
  .details {
    margin: 3rem;
    font-size: 2rem;
  }
}
</style>