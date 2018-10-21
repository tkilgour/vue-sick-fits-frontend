<template>
  <div class="columns">
    <Signup />
    <Signup />
    <Signup />
  </div>
</template>

<script>
import Signup from "../components/Signup";

export default {
  name: "SignupPage",
  components: {
    Signup
  }
}
</script>

<style lang="scss" scoped>
.columns {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  grid-gap: 20px;
}
</style>
