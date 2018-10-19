<template>
  <ApolloMutation
    :mutation="require('@/apollo/mutations/deleteItem.gql')"
    :variables="{id}"
    :update="update"
  >
    <template slot-scope="{ mutate, error }">
      <button @click="deleteItem(mutate)">{{ buttonText }}</button>
    </template>
  </ApolloMutation>
</template>

<script>
export default {
  name: 'DeleteItem',
  props: {
    id: String,
    buttonText: {
      type: String,
      default: 'Delete'
    }
  },
  methods: {
    deleteItem(deleteItemMutation) {
      if (confirm('Are you sure you want to delte this item?')) {
        deleteItemMutation();
      }
    },
    update(cache, payload) {
      const ALL_ITEMS_QUERY = require('@/apollo/queries/allItems.gql');
      const data = cache.readQuery({ query: ALL_ITEMS_QUERY });
      data.items = data.items.filter(
        item => item.id !== payload.data.deleteItem.id
      );
      cache.writeQuery({ query: ALL_ITEMS_QUERY, data })
    }
  }
}
</script>

<style lang="scss" scoped>
button {
  background: white;
  border: 0;
  font-size: 1rem;
  padding: 1rem;
  width: 100%;
  height: 100%;
}
</style>