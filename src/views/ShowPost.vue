<template>
  <div class="posts-show">
    <h1>{{ message }}</h1>
    <h1>title: {{ post.title }}</h1>
    <h1>body: {{ post.body }}</h1>
    <p><img v-bind:src="post.image"></p>
  </div>
</template>

<style>
img {
  width: 200px;
}
</style>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      message: "See post",
      post: {}
    };
  },
  created: function() {
    this.postShow();
  },
  methods: {
    postShow: function() {
      console.log('showing one post');
      console.log(this.$route);
      // get data from rails
      axios.get(`/posts/${this.$route.params.id}`).then(response => {
        console.log(response.data);
        this.post = response.data;
      })
    }
  },
};
</script>