<template>
  <div>
    <Nav class="mx-auto sticky top-0" />
    <div class="w-4/5 sm:w-1/2 mx-auto my-5">
      <h3 class="my-5 font-bold text-4xl">{{ member.Title }}</h3>
      <img
        :src="`http://localhost:1337${member.image.url}`"
        class="max-h-screen"
      />
      <p class="mt-5 font-bold">
        written by {{ member.users_permissions_user.username }}
      </p>
      <div class="my-5" v-html="$md.render(member.Content)"></div>
      <button
        v-if="
          $strapi.user && member.users_permissions_user.id === $strapi.user.id
        "
        class="button--grey"
        @click="deletePost(member.id)"
      >
        Delete
      </button>
    </div>
  </div>
</template>
<script>
export default {
  async asyncData({ $strapi, route }) {
    const id = route.params.id
    const member = await $strapi.$members.findOne(id)
    return { member }
  },
  methods: {
    async deletePost(id) {
      await this.$strapi.$members.delete(id)
      this.$nuxt.$router.push('/members')
    },
  },
  middleware({ $strapi, redirect }) {
    if ($strapi.user === null) {
      redirect('/members')
    }
  },
}
</script>
<style scoped>
h1 {
  font-weight: 700;
  font-size: 2rem;
  margin: 0.5em 0;
}
</style>