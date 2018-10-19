<template>
  <div class="item-styles">
    <img v-if="item.image" :src="item.image" :alt="item.title">
    <h3 class="title">
      <nuxt-link :to="{ path: '/item', query: { id: item.id }}">{{item.title}}</nuxt-link>
    </h3>
    <span class="price-tag">{{ this.formatMoney(item.price) }}</span>
    <p>{{ item.description }}</p>
    <div class="buttonList">
      <nuxt-link :to="{ path: '/update', query: { id: item.id }}">Edit ✏️</nuxt-link>
      <button>Add To Cart</button>
      <button>Delete</button>
    </div>
  </div>
</template>

<script>
import formatMoney from "../lib/formatMoney";

export default {
  name: 'Item',
  props: {
    item: Object
  },
  methods: {
    formatMoney
  }
}
</script>

<style lang="scss" scoped>
@import '@/assets/scss/_vars.scss';
.title {
  margin: 0 1rem;
  text-align: center;
  transform: skew(-5deg) rotate(-1deg);
  margin-top: -3rem;
  text-shadow: 2px 2px 0 rgba(0, 0, 0, 0.1);
  a {
    background: $red;
    display: inline;
    line-height: 1.3;
    font-size: 4rem;
    text-align: center;
    color: white;
    padding: 0 1rem;
  }
}

.item-styles {
  background: white;
  border: 1px solid $offWhite;
  box-shadow: $bs;
  position: relative;
  display: flex;
  flex-direction: column;
  img {
    width: 100%;
    height: 400px;
    object-fit: cover;
  }
  p {
    font-size: 12px;
    line-height: 2;
    font-weight: 300;
    flex-grow: 1;
    padding: 0 3rem;
    font-size: 1.5rem;
  }
  .buttonList {
    display: grid;
    width: 100%;
    border-top: 1px solid $lightgrey;
    grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
    grid-gap: 1px;
    background: $lightgrey;
    & > * {
      background: white;
      border: 0;
      font-size: 1rem;
      padding: 1rem;
    }
  }
}

.price-tag {
  background: $red;
  transform: rotate(3deg);
  color: white;
  font-weight: 600;
  padding: 5px;
  line-height: 1;
  font-size: 3rem;
  display: inline-block;
  position: absolute;
  top: -3px;
  right: -3px;
}
</style>
