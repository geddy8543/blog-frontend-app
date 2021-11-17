<template>
  <div>
    <h1>{{ message }}</h1>

    <div
      v-for="post in posts"
      v-on:click="currentPost = post"
      v-bind:class="{ selected: post === currentPost }"
      :key="post.id"
    >
      <h3>{{ post.title }}</h3>
      <router-link :to="`/posts/${post.id}`">
        <img :src="post.image" :alt="post.title" />
      </router-link>
      <p>Title: {{ post.title }}</p>
      <p>Description: {{ post.body }}</p>
    </div>
  </div>
</template>

<style>
.selected {
  color: blueviolet;
  background-color: bisque;
}
</style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Welcome to the Posts!!",
      posts: [],
      currentPost: {},
    };
  },
  created: function () {
    this.indexPosts();
  },
  methods: {
    indexPosts: function () {
      axios.get("/posts").then((response) => {
        this.posts = response.data;
        console.log("All posts", this.posts);
      });
    },
  },
};
</script>
