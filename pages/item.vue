<template>
  <SingleItem :id="id" :item="item" />
</template>

<script>
import SingleItem from '../components/SingleItem';
import SINGLE_ITEM_QUERY from '../apollo/queries/singleItem.gql';

export default {
  name: "Item",
  components: {
    SingleItem
  },
  async asyncData({app, query}) {
    const { data } = await app.apolloProvider.defaultClient.query({
      query: SINGLE_ITEM_QUERY,
      variables: { id: query.id }
    })
    return {
      item: data.item,
      id: query.id
    }
  }
}
</script>
