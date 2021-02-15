 <template>
 <div class="px-4">
  <div class="bg-gray-100 rounded-md border shadow-lg max-w-md mx-auto text-center my-12 mx-4">
    <div v-show="error !== ''" class="py-6 px-4 bg-red-200  text-red-500 rounded-t-md ">
      <p>{{ error }}</p>
    </div>
    <h1 class="text-4xl text-gray-400 tracking-wider font-bold mt-5">Signup</h1>
    <div class="p-4">
    <form @submit="createUser">
      <div>
        <input
          v-model="email"
          required
          class="p-3 my-5 rounded-md border bg-gray-100 focus:shadow-xl focus:outline-none focus:bg-white shadow-md w-full"
          type="email"
          placeholder="email"
        />
      </div>
      <div>
        <input
          v-model="username"
          required
          class="p-3 my-5 rounded-md border bg-gray-100 focus:shadow-xl focus:outline-none focus:bg-white shadow-md w-full"
          type="text"
          placeholder="username"
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
          {{loading ? 'Please wait...' : 'Signup' }}
        </button>
      </div>
       <div>
        <p>Already a member? <n-link class="text-blue-500" to="/login">Login</n-link></p>
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
      email: '',
      username: '',
      password: '',
      error: '',
      loading: false,
    }
  },
  methods: {
    async createUser(e) {
      this.error = '';
      this.loading = true;
      e.preventDefault()
      try {
        const newUser = await this.$strapi.register({
          email: this.email,
          username: this.username,
          password: this.password,
        })
        console.log(newUser)
        if (newUser !== null) {
          this.error = '';
          this.loading = false;
          this.$nuxt.$router.push('/members')
        }
      } catch (error) {
        this.loading = false;
        this.error = error.message
      }
    },
  },
  middleware: 'authenticated',
}
</script>