<template>
  <div>
    <Navbar class="fixed mx-auto sticky top-0" />

    <h1 class="uppercase tracking-widest font-semibold text-xl text-center my-6">All members</h1>
    <div
      v-if="$apollo.queries.members.loading"
      class="w-full h-64 px-6 flex justify-center items-center"
    >
      Members info still loading
    </div>
    <div v-else-if="members === null" class="w-full h-64 px-6 flex justify-center items-center">
      Members not loaded yet
    </div>
     <div v-else class="sm:grid md:grid-cols-2 lg:grid-cols-3 md:gap-2 px-4">
    <div v-for="(member, i) in members" :key="i">     
      <div class="w-full max-w-sm mx-auto my-6 border rounded-md shadow-lg overflow-hidden">
        <div class="bg-blue-500 p-4 text-gray-200">
        <h1 class="font-semibold tracking-wider text-lg">{{ member.name }}</h1>
        <h3>{{ member.position }}</h3>
        <h3>{{ member.email }}</h3>
         </div>
         <div class="p-4">
        <p class="font-semibold tracking-wider">Bio</p>       
        <p>{{ member.bio }}</p>
        </div>
      </div>
      </div>
      </div>
    </div>
  
</template>
<script>
import membersQuery from "~/apollo/queries/member/members";
export default {
  data() {
    return {
      members: [],
      query: "",
      error: null,
    };
  },
  apollo: {
    members: {
      prefetch: true,
      query: membersQuery,
    },
    // error(error) {
    //   this.error = JSON.stringify(error.message);
    // }
  },
};
</script>
<style></style>