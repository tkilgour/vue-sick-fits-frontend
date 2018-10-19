<template>
  <SingleItem :id="this.$route.query.id" />
</template>

<script>
import SingleItem from '../components/SingleItem';

export default {
  name: "Item",
  components: {
    SingleItem
  }
}
</script>
