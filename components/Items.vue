<template>
  <div class="center">
    <Pagination :count="count" />
      <div v-if="items" class="items-list">
        <Item 
          v-for="item of items" 
          :key="item.id" 
          :item="item" 
          class="item"
        />
      </div>
    <Pagination :count="count" />
  </div>
</template>

<script>
import gql from 'graphql-tag'
import Item from './Item'
import Pagination from "./Pagination";

export default {
  name: "Items",
  props: {
    items: Array,
    count: Number
  },
  components: {
    Item,
    Pagination
  },
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
