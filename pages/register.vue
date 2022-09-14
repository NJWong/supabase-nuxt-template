<template>
  <div class="text-white w-[600px] mx-auto rounded border border-zinc-800 p-8">
    <form class="flex flex-col gap-4" @submit.prevent="registerUser">
      <h1 class="text-2xl">Register to NUXT_APP</h1>
      <div v-if="showError" class="rounded bg-red-300 text-red-700 px-4 py-2">
        <p>{{ errorMsg }}</p>
      </div>
      <div class="flex flex-col gap-2">
        <label class="text-sm">Email</label>
        <input v-model="email" type="text" class="px-4 py-2 rounded bg-zinc-900 border border-zinc-800 outline-none focus:ring-1 focus:ring-zinc-500 focus:bg-zinc-800/50" />
      </div>
      <div class="flex flex-col gap-2">
        <label class="text-sm">Password</label>
        <input v-model="password" type="password" class="px-4 py-2 rounded bg-zinc-900 border border-zinc-800 outline-none focus:ring-1 focus:ring-zinc-500 focus:bg-zinc-800/50" />
      </div>
      <button :disabled="loading" type="submit" class="px-4 py-2 rounded bg-green-600 hover:bg-green-600/90">Register</button>
    </form>
  </div>
</template>

<script setup lang="ts">
import { ApiError } from '@supabase/gotrue-js';

const client = useSupabaseClient()
const user = useSupabaseUser()

const email = ref('')
const password = ref('')
const loading = ref(false)
const showError = ref(false)
const errorMsg = ref('')

const registerUser = async () => {
  try {
    showError.value = false
    loading.value = true

    const { session, error } = await client.auth.signUp({ email: email.value, password: password.value })
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