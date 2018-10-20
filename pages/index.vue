<template>
  <Items :items="items" :count="count" />
</template>

<script>
import Items from '../components/Items'
import ALL_ITEMS_QUERY from '../apollo/queries/allItems.gql';

export default {
  name: 'Home',
  components: {
    Items
  },
  async asyncData({app}) {
    const { data } = await app.apolloProvider.defaultClient.query({ query: ALL_ITEMS_QUERY})
    return {
      count: data.itemsConnection.aggregate.count,
      items: data.items
    }
  }
}
</script>

<style>
</style>