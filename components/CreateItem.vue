<template>
  <ApolloMutation 
    :mutation="require('@/apollo/mutations/createItem.gql')" 
    :variables="{title, description, image, largeImage, price}" 
    @done="handleMutate($event)"
  >
    <template slot-scope="{ mutate, loading, error }">
      <form @submit.prevent="mutate">
        <Error :error="error" />
        <fieldset :disabled="loading" :aria-busy="loading">
          <label for="file">
            Image
            <input
              type="file"
              id="file"
              name="file"
              placeholder="Upload an image"
              required
              @change="uploadFile"
            />
            <img v-if="image" width="200" :src="image" alt="Upload Preview">
          </label>
          <label for="title">
            Title
            <input
              type="text"
              id="title"
              name="title"
              placeholder="Title"
              required
              v-model.trim="title"
            />
          </label>
          <label for="price">
            Price
            <input
              type="number"
              id="price"
              name="price"
              placeholder="Price"
              required
              v-model.number="price"
            />
          </label>
          <label for="description">
            Description
            <textarea
              id="description"
              name="description"
              placeholder="Description"
              required
              v-model.trim="description"
            />
          </label>
          <button type="submit">Submit</button>
        </fieldset>
      </form>
    </template>
  </ApolloMutation>
</template>

<script>
import gql from 'graphql-tag'
import Error from './ErrorMessage'

export default {
  name: 'CreateItem',
  components: {
    Error
  },
  data() {
    return {
      title: "La Croix – Lemon",
      description: "Delicious Lemony goodness – naturally essenced, of course!",
      image: "",
      largeImage: "",
      price: 87
    }
  },
  methods: {
    async uploadFile(e) {
      console.log('uploading file...');
      const files = e.target.files;
      const data = new FormData();
      data.append('file', files[0]);
      data.append('upload_preset', 'sick-fits');

      const res = await fetch('https://api.cloudinary.com/v1_1/tkilgour/image/upload', {
        method: 'POST',
        body: data
      });
      const file = await res.json();
      console.log(file);
      this.image = file.secure_url;
      this.largeImage = file.eager[0].secure_url;
    },
    handleMutate(res) {
      this.$router.push({
        path: '/item',
        query: { id: res.data.createItem.id }
      })
    }
  }
}
</script>

<style lang="scss" scoped>
@import '@/assets/scss/_form.scss';
</style>
