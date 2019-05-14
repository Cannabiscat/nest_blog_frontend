<template>
  <div>
    <div class="col-md-12 form-wrapper">
      <h2>Create post</h2>
      <form id="create-post-form" @submit.prevent="createPost">
        <div class="form-group col-md-12">
          <label for="title">Title</label>
          <input
            type="text"
            id="title"
            v-model="title"
            name="title"
            class="form-control"
            placeholder="Enter title"
          >
          <div class="form-group col-md-12">
            <label for="description">Description</label>
            <input
              type="text"
              id="description"
              v-model="description"
              name="description"
              placeholder="Enter description"
            >
          </div>
          <div class="form-group col-md-12">
            <label for="body">Write content</label>
            <textarea id="body" cols="30" rows="5" v-model="body" class="fordm-control"></textarea>
          </div>
          <div class="form-group col-md-12">
            <label for="author">Author</label>
            <input type="text" class="form-control" id="author" v-model="author">
          </div>
          <div class="form-group pull-right col-md-4">
            <button class="btn btn-success" type="submit">Create Post</button>
          </div>
        </div>
      </form>
    </div>
  </div>
</template>
<script>
import axios from "axios";
import { server } from "../../utils/helper";
import router from "../../router";
export default {
  data() {
    return {
      title: "",
      description: "",
      author: "",
      body: "",
      date_posted: ""
    };
  },
  created() {
    this.date_posted = new Date().toLocaleDateString;
  },
  methods: {
    createPost() {
      let postData = {
        title: this.title,
        description: this.description,
        author: this.author,
        body: this.body,
        date_posted: this.date_posted
      };
      this.__submitToServer(postData);
    },
    __submitToServer(data) {
      axios.post(`${server.baseURI}/blog/post`, data).then(data => {
        router.push({ name: "home " });
      });
    }
  }
};
</script>
