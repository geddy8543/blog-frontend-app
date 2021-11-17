<template>
  <div class="posts-show">
    <h1>{{ post.title }}</h1>
    <img :src="post.image_url" :alt="post.title" />
    <p>{{ post.body }}</p>
    <router-link v-bind:to="`/posts/${post.id}/edit`">Edit this post</router-link>
    |
    <router-link to="/">Back to all posts</router-link>
  </div>
</template>

<style></style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      post: {},
    };
  },
  created: function () {
    axios.get("/posts/" + this.$route.params.id).then((response) => {
      this.post = response.data;
    });
  },
  methods: {},
};
</script>
