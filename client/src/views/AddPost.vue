<template>
  <v-container>
    <v-row no-gutters>
      <v-col sm="10" class="mx-auto">
        <v-card>
          <v-card-title class='d-flex justify-center'>Content</v-card-title>
          <v-form
            ref="form"
            @submit.prevent="submitForm"
            class="pa-4"
            enctype="multipart/form-data"
          >
            <v-text-field
              label="Title"
              v-model="post.title"
              prepend-icon="mdi-note"
              :rules="rules"
            ></v-text-field>
            <v-text-field
              label="Category"
              v-model="post.category"
              prepend-icon="mdi-view-list"
              :rules="rules"
            ></v-text-field>
            <v-textarea
              label="Content"
              v-model="post.content"
              prepend-icon="mdi-note-plus"
              :rules="rules"
            ></v-textarea>
            <v-file-input
              :rules="rules"
              @change="selectFile"
              show-size
              counter
              multiple
              label="Select Image"
            ></v-file-input>
            <v-btn type="submit" class="mt-4 mx-2" color="primary"
              >Add Review
            </v-btn>
          </v-form>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import API from "../api";
export default {
  data() {
    return {
      rules: [(value) => !!value || "This field is required!"],
      post: {
        title: "",
        category: "",
        content: "",
        image: "",
      },
      image: "",
    };
  },
  methods: {
    selectFile(file) {
      this.image = file[0];
    },
    async submitForm() {
      const formData = new FormData();
      formData.append("title", this.post.title);
      formData.append("category", this.post.category);
      formData.append("content", this.post.content);
      formData.append("image", this.image); //image is the name of the input field in the form
      if (this.$refs.form.validate()) {
        const response = await API.addPost(formData);
        this.$router.push({
          name: "home",
          params: { message: response.message },
        });
      }
    },
  },
};
</script>