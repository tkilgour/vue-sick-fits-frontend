<template>
  <Items :items="items" :count="count" />
</template>

<script>
import Items from '../components/Items'
import ALL_ITEMS_QUERY from '../apollo/queries/allItems.gql';
import PAGINATION_QUERY from '../apollo/queries/pagination.gql';

export default {
  name: 'Home',
  components: {
    Items
  },
  async asyncData({app}) {
    const items = await app.apolloProvider.defaultClient.query({ query: ALL_ITEMS_QUERY})
    const pagination = await app.apolloProvider.defaultClient.query({ query: PAGINATION_QUERY})
    return {
      items: items.data.items,
      count: pagination.data.itemsConnection.aggregate.count,
    }
  }
}
</script>

<style>
</style>