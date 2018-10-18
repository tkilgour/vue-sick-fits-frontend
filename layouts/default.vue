<template>
  <div class="styled-page">
    <div class="meta"/>
    <Header />
    <div class="inner">
      <nuxt/>
    </div>
  </div>
</template>

<script>
import Header from "../components/Header";

export default {
  components: {
    Header
  }
}
</script>


<style lang="scss" scoped>
@import '@/assets/scss/_vars.scss';

.styled-page {
  background: white;
  color: $black;
}

.inner {
  max-width: $maxWidth;
  margin: 0 auto;
  padding: 2rem;
}
</style>
