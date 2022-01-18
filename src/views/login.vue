<template>
  <div class="mt-8">
    <div class="container mx-auto px-8">
      <div class="row flex justify-center">
        <span class="font-semibold text-3xl">Login</span>
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
          <button
            type="submit"
            class="py-3 text-center w-full bg-purple-500 text-white rounded-lg"
          >
            Sign Up
          </button>
        </div>
      </form>
      <!-- direction -->
      <div class="w-full text-center mt-6">
        <span class="font-semibold">I'm a new member.</span>
        <span class="ml-1">
          <router-link
            :to="{ name: 'Register', param: {} }"
            class="text-purple-500 font-bold"
            >Sign Up</router-link
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
    };
  },
  methods: {
    onSubmit() {
      const data = {
        userName: this.userName,
        passWord: this.passWord,
      };

      if (data.userName == "") {
        alert("UseName Can not be empty");
        return data;
      }
      if (data.passWord == "") {
        alert("PassWord Can not be empty");
        return data;
      }

      axios
        .post("http://localhost:3000/user/login", data)
        .then((res) => {
          this.$router.push('/');
          alert("Login Success!");
          console.log(res);
          localStorage.setItem('token', res.data.Token);
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
};
</script>
