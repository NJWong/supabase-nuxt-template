<template>
  <div class="flex items-center justify-between px-8 py-4 text-sm text-zinc-100 border-b border-zinc-800">
    <NuxtLink to="/">Home</NuxtLink>
    <nav v-if="user" class="flex gap-4 items-center">
      <NuxtLink to="/profile" class="px-4 py-2 hover:text-rose-500">
        Profile
      </NuxtLink>
      <button class="px-4 py-2 hover:text-rose-500" @click="handleLogOut">
        Log out
      </button>
    </nav>
    <nav v-else class="flex gap-2 items-center">
      <NuxtLink to="/login" class="px-4 py-1 rounded border border-zinc-700 bg-zinc-800 hover:bg-zinc-700/50">
        Log in
      </NuxtLink>
      <NuxtLink to="/register" class="px-4 py-1 rounded bg-emerald-600 hover:bg-emerald-500/90">
        Register
      </NuxtLink>
    </nav>
  </div>
</template>

<script setup lang="ts">
const user = useSupabaseUser()
const client = useSupabaseClient()

const handleLogOut = async () => {
  await client.auth.signOut()
  navigateTo('/login')
}
</script>