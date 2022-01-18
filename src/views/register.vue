<template>
  <div class="mt-8">
    <div class="container mx-auto px-8">
      <div class="row flex justify-center">
        <span class="font-semibold text-3xl">Register</span>
      </div>
      <!-- Form -->
      <form
        @submit.prevent="onSubmit"
        class="flex flex-col justify-start space-y-6"
      >
        <div class="row">
          <label class="flex flex-col" for="UserName">
            <span class="font-semibold">User Name</span>
            <input
              id="UserName"
              v-model="userName"
              class="px-4 py-3 rounded-lg border border-gray-100 mt-1"
              type="text"
              placeholder="UserName"
              autocomplete="username"
            />
          </label>
        </div>
        <div class="row">
          <label class="flex flex-col" for="PassWord">
            <span class="font-semibold">PassWord</span>
            <input
              id="Password"
              v-model="passWord"
              class="px-4 py-3 rounded-lg border border-gray-100 mt-1"
              type="password"
              placeholder="PassWord"
              autocomplete="current-password"
            />
          </label>
        </div>
        <div class="row">
          <label class="flex flex-col" for="email">
            <span class="font-semibold">email</span>
            <input
              id="email"
              v-model="email"
              class="px-4 py-3 rounded-lg border border-gray-100 mt-1"
              type="email"
              placeholder="...@gmail.com"
              autocomplete="email"
            />
          </label>
        </div>
        <div class="row">
          <button
            v-if="!isPending"
            type="submit"
            class="py-3 text-center w-full bg-purple-500 text-white rounded-lg"
          >
            Sign Up
          </button>
          <button
            v-else
            type="submit"
            class="py-3 text-center w-full bg-gray-500 text-white rounded-lg cursor-not-allowed"
            disabled
          >
            Loading...
          </button>
        </div>
      </form>
      <!-- direction -->
      <div class="w-full text-center mt-6">
        <span class="font-semibold">I'm ready login now.</span>
        <span class="ml-1">
          <router-link
            :to="{ name: 'Login', param: {} }"
            class="text-purple-500 font-bold"
            >Sign In</router-link
          >
        </span>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Register",
  data() {
    return {
      userName: "",
      passWord: "",
      email: "",
    };
  },
  methods: {
    onSubmit() {
      const data = {
        userName: this.userName,
        passWord: this.passWord,
        email: this.email,
      };

      if (data.userName == "") {
        alert("UseName Can not be empty");
        return data;
      }
      if (data.passWord == "") {
        alert("PassWord Can not be empty");
        return data;
      }
      if (data.email == "") {
        alert("Email Can not be empty");
        return data;
      }

      axios
        .post("http://localhost:3000/user/create", data)
        .then((res) => {
          alert("Create Success!");
          console.log(res);
          this.$router.push('Login');
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
};
</script>
