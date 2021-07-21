<template>
  <div class="posts-new">
    <form v-on:submit.prevent="submit()">
      <h1>Create a new Post</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Title:</label>
        <input type="text" v-model="newPost.title" />
      </div>
      <div>
        <label>Body:</label>
        <input type="text" v-model="newPost.body" />
      </div>
      <div>
        <label>Image:</label>
        <input type="text" v-model="newPost.image" />
      </div>
       <input type="submit" value="Submit" />
    </form>
  </div>
</template>

<script>
  import axios from "axios";
  export default {
    data: function () {
      return {
        newPost: {},
        errors: [],
      };
    },
    methods: {
      submit: function () {
        axios
          .post("/posts", this.newPost)
          .then((response) => {
            console.log(response.data);
            this.$router.push("/posts");
          })
          .catch((error) => {
            this.errors = error.response.data.errors;
          });
      },
    },
  };
</script>