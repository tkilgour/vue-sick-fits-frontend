<template>
  <div class="pagination-styles">
    <nuxt-link :to="{
      path: 'items',
      query: { page: page - 1 }
    }" class="prev" :aria-disabled="page <= 1">
      ← Prev
    </nuxt-link>
    <p>
      Page {{page}} of {{pages}}
    </p>
    <p>{{count}} Item{{ count > 1 ? 's' : ''}} Total</p>
    <nuxt-link :to="{
      path: 'items',
      query: { page: page + 1 }
    }" class="next" :aria-disabled="page >= pages">
      Next →
    </nuxt-link>
  </div>
</template>

<script>
import { perPage } from "../config";

export default {
  name: 'Pagination',
  props: {
    count: Number
  },
  computed: {
    page() {
      return parseFloat(this.$route.query.page) || 1;
    },
    pages() {
      return Math.ceil(this.count / perPage);
    }
  }
}
</script>

<style lang="scss" scoped>
@import '@/assets/scss/_vars.scss';

.pagination-styles {
  text-align: center;
  display: inline-grid;
  grid-template-columns: repeat(4, auto);
  align-items: stretch;
  justify-content: center;
  align-content: center;
  margin: 2rem 0;
  border: 1px solid $lightgrey;
  border-radius: 10px;
  & > * {
    margin: 0;
    padding: 15px 30px;
    border-right: 1px solid $lightgrey;
    &:last-child {
      border-right: 0;
    }
  }
  a[aria-disabled='true'] {
    color: grey;
    pointer-events: none;
  }
}
</style>
