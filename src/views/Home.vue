<template>
  <div id="home" class="flex flex-col justify-center  m-2">
    <h1 class="text-3xl">BLOG VMO</h1>
  </div>
  <div id="home" class="flex flex-col justify-center align-middle m-2">
    <div
      v-for="(blog, index) in blogs"
      :key="index"
      class="rounded-lg border border-gray-200 m-2 p-2"
    >
      <h1 class="text-2xl">{{ blog.blogName }}</h1>
      <h2>Title: {{ blog.title }}</h2>
      <h3>Content: {{ blog.content }}</h3>
      <h3>Images: {{ blog.images }}</h3>
      <h3>Comments: {{ blog.comments }}</h3>
      <form @submit.prevent="addComment">
        <div class="row">
          <input type="text" placeholder="Comments" v-model="comments" class="m-2" />
        </div>
        <div class="row">
          <button
            type="submit"
            class="p-0.5 text-center w-50 bg-purple-500 text-white rounded-lg"
          >
           Comments
          </button>
        </div>
      </form>
    </div>
  </div>
  <button
    @click="clearToken()"
    type="submit"
    class="p-0.5 text-center w-50 bg-purple-500 text-white rounded-lg m-4 flex  justify-center items-center">
    Clear Token
  </button>

    <div class="w-full text-center mt-6">
      <span class="ml-1">
        <router-link
          :to="{ name: 'Login', param: {} }"
          class="text-purple-500 font-bold"
        >
        Sign In
        </router-link>
      </span>
    </div>
</template>

<script>
import axios from "axios";

export default {
  name: "home",
  data() {
    return {
      blogs: null,
    };
  },

  mounted() {
    axios.get("http://localhost:3000/blog/get").then((resp) => {
      console.log(this.id_blog);
      this.blogs = resp.data;
    });
  },
  
  methods: {
    addComment() {
      const data = {
        comments: this.comments,
      };
      const tokenKey = localStorage.getItem('token');

      const headersRequest = {
        'Content-Type': 'application/json',
         Authorization: `Bearer ${tokenKey}`,
      };
        console.log(headersRequest)

      if(!tokenKey){
        alert('You must be logged in to Comment')
        this.$router.push('Login');
      }else{
              axios
        .put("http://localhost:3000/blog/update/9c9aa5f3-1f6b-4822-8a2a-f5c53b7852fe",
         data,
         { headers: headersRequest },
         )
        .then((res) => {
          console.log(res);
        })
        .catch((err) => {
          console.log(err);
        });
      }
    },

    clearToken(){
      localStorage.clear();
      alert('Cleared Token')
      console.log('clear Token')
    }
  },
};
</script>
