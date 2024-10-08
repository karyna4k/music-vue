<script setup lang="ts">
import { storeToRefs } from 'pinia'
import { useModalStore } from '@/stores/modal'
import { ref } from 'vue'
import Login from '@/components/LoginForm.vue'
import Register from '@/components/RegisterForm.vue'

const { isOpen: modalVisibility, hiddenClass } = storeToRefs(useModalStore())

const tab = ref<'Login' | 'Register'>('Login')
const tabs = { Login, Register }
</script>

<template>
  <!-- Auth Modal -->
  <div id="modal" class="fixed z-10 inset-0 overflow-y-auto" :class="hiddenClass">
    <div
      class="flex items-end justify-center min-h-screen pt-4 px-4 pb-20 text-center sm:block sm:p-0"
    >
      <div class="fixed inset-0 transition-opacity">
        <div class="absolute inset-0 bg-gray-800 opacity-75"></div>
      </div>

      <!-- This element is to trick the browser into centering the modal contents. -->
      <span class="hidden sm:inline-block sm:align-middle sm:h-screen">&#8203;</span>

      <div
        class="inline-block align-bottom bg-white rounded-lg text-left overflow-hidden shadow-xl transform transition-all sm:my-8 sm:align-middle sm:max-w-lg sm:w-full"
      >
        <!-- Add margin if you want to see some of the overlay behind the modal-->
        <div class="py-4 text-left px-6">
          <!--Title-->
          <div class="flex justify-between items-center pb-4">
            <p class="text-2xl font-bold">Your Account</p>
            <!-- Modal Close Button -->
            <button class="modal-close cursor-pointer z-50" @click="modalVisibility = false">
              <i class="fas fa-times"></i>
            </button>
          </div>

          <!-- Tabs -->
          <div class="flex flex-wrap mb-4">
            <button
              v-for="(_, t) in tabs"
              :key="t"
              class="grow rounded py-3 px-4 transition"
              :class="{
                'hover:text-white text-white bg-blue-600': tab === t,
                'hover:text-blue-600': tab !== t
              }"
              @click="tab = t"
            >
              {{ t }}
            </button>
          </div>

          <component :is="tabs[tab]" />
        </div>
      </div>
    </div>
  </div>
</template>
