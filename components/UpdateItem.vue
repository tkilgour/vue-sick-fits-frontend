<template>
  <ApolloQuery 
    :query="require('@/apollo/queries/singleItem.gql')" 
    :variables="{id: item.id}"
  >
    <template slot-scope="{ result: { data, error }, isLoading }">
      <p v-if="isLoading">Loading...</p>
      <p v-else-if="!data.item">No Item Found for ID {{item.id}}</p>
      <ApolloMutation
        v-else
        :mutation="require('@/apollo/mutations/updateItem.gql')" 
        :variables="item" 
      >
        <template slot-scope="{ mutate, loading, error }">
          <form @submit.prevent="updateItem(mutate)">
            <Error :error="error" />
            <fieldset :disabled="loading" :aria-busy="loading">
              <label for="title">
                Title
                <input
                  type="text"
                  id="title"
                  name="title"
                  placeholder="Title"
                  required
                  :value="data.item.title"
                  @input="handleChange"
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
                  :value="data.item.price"
                  @input="handleChange"
                />
              </label>
              <label for="description">
                Description
                <textarea
                  id="description"
                  name="description"
                  placeholder="Description"
                  required
                  :value="data.item.description"
                  @input="handleChange"
                />
              </label>
              <button type="submit">Sav{{ loading ? 'ing' : 'e'}} Changes</button>
            </fieldset>
          </form>
        </template>
      </ApolloMutation>
    </template>
  </ApolloQuery>
</template>

<script>
import gql from 'graphql-tag'
import Error from './ErrorMessage'

export default {
  name: 'UpdateItem',
  components: {
    Error
  },
  data() {
    return {
      item: {
        id: this.$route.query.id,
      }
    }
  },
  methods: {
    async updateItem(updateItemMutation) {
      console.log('updating item!');
      console.log(this.item);
      updateItemMutation({
        variables: this.item
      });
      console.log("updated!");
    },
    handleChange(e) {
      const { name, type, value } = e.target;
      const val = type === "number" ? parseFloat(value) : value;
      this.item[name] = val ;
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
