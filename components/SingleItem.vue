<template>
  <div>
    <p v-if="!item">No Item Found for {{id}}</p>
    <div v-else class="single-item-styles">
      <img :src="item.largeImage" :alt="item.title">
      <div class="details">
        <h2>Viewing {{ item.title }}</h2>
        <p>{{ item.description }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import Error from "./ErrorMessage";

export default {
  name: "SingleItem",
  head() {
    return {
      title: `Sick Fits | ${this.title}`
    }
  },
  props: {
    id: String,
    item: Object
  },
  components: {
    Error
  },
  data() {
    return {
      title: '...'
    }
  }
}
</script>

<style lang="scss" scoped>
@import '@/assets/scss/_vars.scss';

.single-item-styles {
  max-width: 1200px;
  margin: 2rem auto;
  box-shadow: $bs;
  display: grid;
  grid-auto-columns: 1fr;
  grid-auto-flow: column;
  min-height: 800px;
  img {
    width: 100%;
    height: 100%;
    object-fit: contain;
  }
  .details {
    margin: 3rem;
    font-size: 2rem;
  }
}
</style>