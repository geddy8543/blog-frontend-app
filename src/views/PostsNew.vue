<template>
  <div class="posts-new">
    <form v-on:submit.prevent="createPost()">
      <h1>New Post!</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Title:</label>
        <input type="text" v-model="newPostsParams.title" />
      </div>
      <div>
        <label>Email:</label>
        <input type="email" v-model="newPostsParams.email" />
      </div>
      <div>
        <label>Password:</label>
        <input type="password" v-model="newPostsParams.password" />
      </div>
      <div>
        <label>Password confirmation:</label>
        <input type="password" v-model="newPostsParams.password_confirmation" />
      </div>
      <div>
        <label>Body:</label>
        <input type="text" v-model="newPostParams.body" />
      </div>
      <div>
        <label>Image:</label>
        <input type="image_url" v-model="newPostParams.image" />
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
      newPostParams: {},
      errors: [],
    };
  },

  methods: {
    creatPost: function () {
      console.log("Makin a new post!");
      axios
        .post("/posts".this.newPostParams)
        .then(() => {
          this.$router.push("/posts");
        })
        .catch((error) => console.log(error.response));
    },
  },
};
</script>
