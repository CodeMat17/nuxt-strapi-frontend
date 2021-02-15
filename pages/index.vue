<template>
  <div class="w-full h-screen flex items-center justify-center">
    <div>
      <h1 class="px-4 block text-4xl md:text-6xl font-thin text-center">Welcome To The Nuxtys Club</h1>
      <div class="mt-20 flex justify-center text-center">
        <NuxtLink to="/login" class="w-full max-w-xs block justify-items-center bg-gray-900 text-gray-400 text-4xl rounded-md"> Login </NuxtLink>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  middleware: 'authenticated',
}
</script>