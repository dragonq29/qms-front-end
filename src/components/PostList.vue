<template>
  <div>
    <b-card
      header="테스트 입니다."
      style="max-width: 40rem; margin: auto; margin-top: 10vh;"
      class="mb-2"
      border-variant="info"
      align="left"
    >
      <div>
        <b-form-input
          v-model="newPost.title"
          type="text"
          placeholder="타이틀"
        />
        <b-form-input
          v-model="newPost.content"
          type="text"
          placeholder="컨텐트"
        />
        <b-form-input v-model="newPost.author" type="text" placeholder="어써" />
        <b-button type="submit" variant="primary" v-on:click="createPost()"
          >생성
        </b-button>
      </div>
      <div>
        <b-list-group v-if="postList && postList.length">
          <b-list-group-item
            v-for="post of postList"
            v-bind:data="post.title"
            v-bind:key="post.id"
          >
            {{ post.title }}
          </b-list-group-item>
        </b-list-group>
      </div>
    </b-card>
  </div>
</template>

<script>
import axios from "axios";

let baseUrl = "http://127.0.0.1:8081/api/v1/posts/";
export default {
  name: "hello",
  data: () => {
    return {
      postList: [],
      newPost: {},
    };
  },
  methods: {
    initList: function() {
      axios
        .get(baseUrl + "all")
        .then((response) => {
          this.postList = response.data.map((r) => r);
        })
        .catch((e) => {
          console.log("error : ", e);
        });
    },

    createPost: function() {
      if (this.newPost.title == "") {
        alert("title를 입력해주세요.");
        return;
      }
      if (this.newPost.content == "") {
        alert("content를 입력해주세요.");
        return;
      }
      if (this.newPost.author == "") {
        alert("author를 입력해주세요.");
        return;
      }
      axios
        .post(baseUrl, this.newPost)
        .then(() => {
          this.initList();
        })
        .catch((e) => {
          console.log("error : ", e);
        });
    },
  },
  created() {
    this.initList();
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
