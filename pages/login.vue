<template>
  <div class="text-zinc-300 w-[450px] mx-auto flex flex-col gap-6">
    <h1 class="text-2xl text-center">Log in to NUXT_APP</h1>
    <div v-if="showError" class="rounded text-sm bg-red-900/30 border-red-800 border p-5 text-zinc-300">
      <p>{{ errorMsg }}</p>
    </div>
    <form class="text-zinc-400 flex flex-col gap-4 rounded border border-zinc-700 bg-zinc-800 p-5" @submit.prevent="logIn">
      <div class="flex flex-col gap-2">
        <label class="text-sm">Email</label>
        <input v-model="email" type="text" class="text-zinc-200 px-4 py-2 rounded bg-zinc-900 border border-zinc-700 outline-none focus:ring-1 focus:ring-zinc-500" />
      </div>
      <div class="flex flex-col gap-2">
        <label class="text-sm">Password</label>
        <input v-model="password" type="password" class="text-zinc-200 px-4 py-2 rounded bg-zinc-900 border border-zinc-700 outline-none focus:ring-1 focus:ring-zinc-500" />
      </div>
      <button :disabled="loading" type="submit" class="text-white px-4 py-2 rounded bg-emerald-600 hover:bg-emerald-500/90 disabled:bg-emerald-400 disabled:cursor-not-allowed">
        {{ loading ? 'Loading...' : 'Log in'}}
      </button>
    </form>
    <div class="border rounded border-zinc-700 p-3 bg-zinc-800">
      <p class="text-center text-sm text-zinc-300">Don't have an account? <NuxtLink class="underline text-sky-600" to="/register">Register here</NuxtLink></p>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ApiError } from '@supabase/gotrue-js';

const client = useSupabaseClient()

const email = ref('')
const password = ref('')
const loading = ref(false)
const showError = ref(false)
const errorMsg = ref('')

const logIn = async () => {
  try {
    loading.value = true

    const { session, error } = await client.auth.signIn({ email: email.value, password: password.value })
    if (error) throw error

    // Make sure the session is set before the `auth` middleware runs
    await client.auth.setSession(session.refresh_token)

    navigateTo('/profile')
  } catch (e) {
    const error = e as ApiError
    showError.value = true
    errorMsg.value = error.message
  } finally {
    loading.value = false
  }
}
</script>