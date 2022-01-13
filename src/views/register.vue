<template>
  <div class="mt-8">
    <div class="container mx-auto px-8">
        <div class="row flex  justify-center">
            <span class="font-semibold text-3xl ">Register</span>
        </div>
      <!-- Form -->
      <form @submit="onSubmit" class="flex flex-col justify-start space-y-6">
        <div class="row">
          <label class="flex flex-col" for="UserName">
            <span class="font-semibold">User Name</span>
            <input id="UserName" class="px-4 py-3 rounded-lg border border-gray-100 mt-1" type="text" placeholder="UserName" autocomplete="username">
          </label>
        </div>
          <div class="row">
          <label class="flex flex-col" for="PassWord">
            <span class="font-semibold">PassWord</span>
            <input id="Password" class="px-4 py-3 rounded-lg border border-gray-100 mt-1" type="text" placeholder="PassWord" autocomplete="current-password">
          </label>
        </div>
          <div class="row">
          <label class="flex flex-col" for="email">
            <span class="font-semibold">email</span>
            <input id="userName" class="px-4 py-3 rounded-lg border border-gray-100 mt-1" type="text" placeholder="...@gmail.com" autocomplete="email">
          </label>
        </div>
        <div class="row">
          <button v-if="isPending" type="submit" class="py-3 text-center w-full bg-purple-500 text-white rounded-lg">
            Sign Up
          </button>
          <button v-else type="submit" class="py-3 text-center w-full bg-gray-500 text-white rounded-lg cursor-not-allowed" disabled>
            Loading...
          </button>
        </div>
      </form>
      <!-- direction -->
      <div class="w-full text-center mt-6">
        <span class="font-semibold">I'm ready login now.</span>
        <span class="ml-1">
          <router-link :to="{ name: 'Login', param: {} }" class="text-purple-500 font-bold">Sign In</router-link>
        </span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  setup() {
    function onSubmit(){}
    return{
      isPending: true,
      onSubmit
    }
  },
}
</script>
