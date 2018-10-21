<template>
  <UpdateItem :item="item" :id="id"/>
</template>

<script>
import UpdateItem from "../components/UpdateItem";
import SINGLE_ITEM_QUERY from '../apollo/queries/singleItem.gql';

export default {
  name: "Update",
  components: {
    UpdateItem
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
