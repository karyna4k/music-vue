<script setup lang="ts">
import { computed, ref } from 'vue'

const schema = {
  email: 'required|min:3|max:100|email',
  password: 'required|min:10|max:100|excluded:password'
}

const loading = ref(false)
const isShowAlert = ref(false)

const alertVariant = computed(() => {
  return isShowAlert.value ? 'bg-blue-500' : 'bg-green-500'
})

const alertMessage = computed(() => {
  return isShowAlert.value
    ? 'Please wait! We are logging you in.'
    : 'Success! You are now logged in'
})

function login(values) {
  loading.value = true
  isShowAlert.value = true

  console.log(values)
}
</script>

<template>
  <!-- Login Form -->
  <div
    v-if="isShowAlert"
    class="text-white text-center font-bold p-4 rounded mb-4"
    :class="alertVariant"
  >
    {{ alertMessage }}
  </div>
  <VeeForm :validation-schema="schema" @submit="login">
    <!-- Email -->
    <div class="mb-3">
      <label class="inline-block mb-2">Email</label>
      <VeeField
        name="email"
        type="email"
        class="block w-full py-1.5 px-3 text-gray-800 border border-gray-300 transition duration-500 focus:outline-none focus:border-black rounded"
        placeholder="Enter Email"
        autocomplete="email"
      />
      <ErrorMessage class="text-red-600" name="email" />
    </div>
    <!-- Password -->
    <div class="mb-3">
      <label class="inline-block mb-2">Password</label>
      <VeeField
        name="password"
        type="password"
        class="block w-full py-1.5 px-3 text-gray-800 border border-gray-300 transition duration-500 focus:outline-none focus:border-black rounded"
        placeholder="Password"
        autocomplete="current-password"
      />
      <ErrorMessage class="text-red-600" name="password" />
    </div>
    <button
      type="submit"
      class="block w-full bg-purple-600 text-white py-1.5 px-3 rounded transition hover:bg-purple-700 disabled:bg-purple-300"
      :disabled="loading"
    >
      Submit
    </button>
  </VeeForm>
</template>
