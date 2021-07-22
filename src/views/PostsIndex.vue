<template>
  <div class="home">
    <div v-for="post in posts">
      <p>{{ post.title }}</p>
      <p>{{ post.body }}</p>
      <p>
        <router-link v-bind:to="`/posts/${post.id}`">
          <img v-bind:src="post.image">
        </router-link>
      </p>
      <hr>
      </div>
  </div>
</template>

<style scoped>
  img {
    width: 200px;
  }
</style>

<script>
import axios from "axios"
export default {
  data: function() {
    return {
      message: "Index of Posts",
      posts: []
    };
  },
  created: function() {
    this.indexPosts();
  },
  methods: {
    indexPosts: function() {
      console.log('indexing posts')
      axios.get("/posts").then(response => {
        console.log(response.data);
        this.posts = response.data;
      });
    }
  },
};
</script>