<template>
  <div class="flex items-center justify-between px-8 py-4 text-sm text-zinc-200 border-b border-zinc-800">
    <NuxtLink to="/">Home</NuxtLink>
    <nav class="flex gap-4 items-center">
      <NuxtLink to="/login" class="px-4 py-2 rounded bg-zinc-800 hover:bg-zinc-700/50">
        Log in
      </NuxtLink>
      <NuxtLink to="/register" class="px-4 py-2 rounded bg-rose-600 hover:bg-rose-600/90">
        Register
      </NuxtLink>
    </nav>
  </div>
</template>