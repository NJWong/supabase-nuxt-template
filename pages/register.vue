<template>
  <div class="text-white w-[600px] mx-auto rounded border border-zinc-800 p-8">
    <form class="flex flex-col gap-4" @submit.prevent="registerUser">
      <h1 class="text-2xl">Register to NUXT_APP</h1>
      <div class="flex flex-col gap-2">
        <label class="text-sm">Email</label>
        <input type="text" class="px-4 py-2 rounded bg-zinc-900 border border-zinc-800 outline-none focus:ring-1 focus:ring-zinc-500 focus:bg-zinc-800/50" />
      </div>
      <div class="flex flex-col gap-2">
        <label class="text-sm">Password</label>
        <input type="password" class="px-4 py-2 rounded bg-zinc-900 border border-zinc-800 outline-none focus:ring-1 focus:ring-zinc-500 focus:bg-zinc-800/50" />
      </div>
      <button type="submit" class="px-4 py-2 rounded bg-green-600 hover:bg-green-600/90">Register</button>
    </form>
  </div>
</template>

<script setup lang="ts">
const registerUser = () => {
  console.log('registerUser')
}
</script>