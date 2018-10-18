<template>
  <div class="center">
    <p>Items!</p>
    <ApolloQuery :query="ALL_ITEMS_QUERY">
      <template slot-scope="{ result: { data, loading, error } }">
        <p v-if="loading">Loading...</p>
        <p v-if="error">Error: {{error.message}}</p>
        <div v-else-if="data" class="items-list">
          <Item v-for="item of data.items" :key="item.id" :item="item" class="item" />
        </div>
      </template>
    </ApolloQuery>
  </div>
</template>

<script>
import gql from 'graphql-tag'
import Item from './Item'

export default {
  name: "Items",
  components: {
    Item
  },
  data() {
    return {
      ALL_ITEMS_QUERY: gql`{
        items {
          id
          title
          price
          description
          image
          largeImage
        }
      }`
    }
  }
}
</script>

<style lang="scss" scoped>
@import '@/assets/scss/_vars.scss';
.center {
  text-align: center;
}

.items-list {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-gap: 60px;
  max-width: $maxWidth;
  margin: 0 auto;
}
</style>
