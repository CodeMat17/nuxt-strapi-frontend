<template>
  <div class="px-4">
    <div
      class="rounded-md border bg-gray-100 shadow-lg max-w-md mx-auto text-center my-12"
    >
      <div
        v-show="error !== ''"
        class="py-6 px-4 bg-red-200 text-red-500 rounded-t-md"
      >
        <p>{{ error }}</p>
      </div>
      <h1 class="text-4xl text-gray-400 tracking-wider font-bold mt-5">
        Login
      </h1>
      <div class="p-4">
        <form @submit="loginUser">
          <div>
            <input
              v-model="identifier"
              required
              class="p-3 my-5 rounded-md border bg-gray-100 focus:shadow-xl focus:outline-none focus:bg-white shadow-md w-full"
              type="email"
              placeholder="email"
            />
          </div>
          <div>
            <input
              v-model="password"
              required
              class="p-3 my-5 rounded-md border bg-gray-100 focus:shadow-xl focus:outline-none focus:bg-white shadow-md w-full"
              type="password"
              placeholder="password"
            />
          </div>
          <div>
            <button
              class="w-full my-4 p-3 bg-gray-900 text-gray-500 font-medium text-xl tracking-wider rounded-md hover:bg-gray-600 hover:text-gray-200"
              type="submit"
            >
              {{ loading ? "Please wait..." : "Login" }}
            </button>
          </div>
          <div>
            <p>
              Not a member yet?
              <n-link class="text-blue-500" to="/signup">Signup</n-link>
            </p>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      identifier: "",
      password: "",
      error: "",
      loading: false,
    };
  },
  methods: {
    async loginUser(e) {
      this.error = "";
      this.loading = true;
      e.preventDefault();
      try {
        const user = await this.$strapi.login({
          identifier: this.identifier,
          password: this.password,
        });
        console.log(user);

        if (user !== null) {
          this.error = "";
          this.$nuxt.$router.push("/members");
          this.loading = false;
        }
      } catch (error) {
        this.loading = false;
        this.error = "Error in login credentials";
      }
    },
  },
  middleware: "authenticated",
};
</script>
<style></style>