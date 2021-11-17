<template>
  <div class="postsindex">
    <form v-on:submit.prevent="updatePost()">
      <h1>Edit Post</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Title:</label>
        <input type="text" v-model="currentPostParams.title" />
      </div>
      <div>
        <label>Body:</label>
        <input type="text" v-model="currentPostParams.body" />
      </div>
      <div>
        <label>Image:</label>
        <input type="image_url" v-model="currentPostParams.image" />
      </div>
      <input type="submit" value="Submit" />
    </form>
  </div>
</template>

<style></style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      currentPostParams: {},
      errors: [],
    };
  },
  created: function () {
    axios.get(`/posts/${this.$route.params.id}`).then((response) => {
      console.log("Post Info", response.data);
      this.currentPostParams = response.data;
    });
  },
  methods: {
    updatePost: function () {
      console.log("Fixin that post!");
      axios
        .patch(`/posts/${this.$route.params.id}`, this.currentPostParams)
        .then((response) => {
          this.$router.push(`/posts/${response.data.id}`);
        })
        .catch((error) => console.log(error.response));
    },
  },
};
</script>
