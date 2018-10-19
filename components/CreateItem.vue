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
@import '@/assets/scss/_vars.scss';
@keyframes loading {
  from {
    background-position: 0 0;
  }

  to {
    background-position: 100% 100%;
  }
}

form {
  box-shadow: 0 0 5px 3px rgba(0, 0, 0, 0.05);
  background: rgba(0, 0, 0, 0.02);
  border: 5px solid white;
  padding: 20px;
  font-size: 1.5rem;
  line-height: 1.5;
  font-weight: 600;
  label {
    display: block;
    margin-bottom: 1rem;
  }
  input,
  textarea,
  select {
    width: 100%;
    padding: 0.5rem;
    font-size: 1rem;
    border: 1px solid black;
    &:focus {
      outline: 0;
      border-color: $red;
    }
  }
  button,
  input[type='submit'] {
    width: auto;
    background: red;
    color: white;
    border: 0;
    font-size: 2rem;
    font-weight: 600;
    padding: 0.5rem 1.2rem;
  }
  fieldset {
    border: 0;
    padding: 0;

    &[disabled] {
      opacity: 0.5;
    }
    &::before {
      height: 10px;
      content: '';
      display: block;
      background-image: linear-gradient(
        to right,
        #ff3019 0%,
        #e2b04a 50%,
        #ff3019 100%
      );
    }
    &[aria-busy='true']::before {
      background-size: 50% auto;
      animation: loading 0.5s linear infinite;
    }
  }
}
</style>
