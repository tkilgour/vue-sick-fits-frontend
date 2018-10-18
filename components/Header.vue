<template>
  <header>
    <div class="bar">
      <h1 class="logo">
        <nuxt-link to="/">Sick Fits</nuxt-link>
      </h1>
      <Nav/>
    </div>
    <div class="sub-bar">
      <p>Search</p>
    </div>
    <div>Cart</div>
  </header>
</template>

<script>
import Nav from './Nav';

export default {
  name: 'Header',
  components: {
    Nav
  }
}
</script>

<style lang="scss" scoped>
@import '@/assets/scss/_vars.scss';
.logo {
  font-size: 4rem;
  margin-left: 2rem;
  position: relative;
  z-index: 2;
  transform: skew(-7deg);
  a {
    padding: 0.5rem 1rem;
    background: $red;
    color: white;
    text-transform: uppercase;
  }
  @media (max-width: 1300px) {
    margin: 0;
    text-align: center;
  }
}

.bar {
  border-bottom: 10px solid $black;
  display: grid;
  grid-template-columns: auto 1fr;
  justify-content: space-betwween;
  align-items: stretch;
  @media (max-width: 1300px) {
    grid-template-columns: 1fr;
    justify-content: center;
  }
}
.sub-bar {
  display: grid;
  grid-template-columns: 1fr auto;
  border-bottom: 1px solid $lightgrey;
}
</style>
