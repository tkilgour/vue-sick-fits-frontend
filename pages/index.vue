<template>
  <Items :items="items" :count="count" />
</template>

<script>
import Items from '../components/Items'
import ALL_ITEMS_QUERY from '../apollo/queries/allItems.gql';
import PAGINATION_QUERY from '../apollo/queries/pagination.gql';
import { perPage } from "../config";

export default {
  name: 'Home',
  components: {
    Items
  },
  async asyncData({app}) {
    const items = await app.apolloProvider.defaultClient.query({
      query: ALL_ITEMS_QUERY,
      variables: {
        skip: (parseFloat(app.context.query.page) || 1) * perPage - perPage
      }
    })
    const pagination = await app.apolloProvider.defaultClient.query({ query: PAGINATION_QUERY})
    return {
      items: items.data.items,
      count: pagination.data.itemsConnection.aggregate.count,
    }
  },
  watchQuery: ['page']
}
</script>
