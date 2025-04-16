<template>
  <div class="bg-white">
    <div class="flex min-h-full flex-col justify-center px-6 py-12 lg:px-8">
      <div class="sm:mx-auto sm:w-full sm:max-w-sm">
        <h2 class="mt-10 text-center text-2xl font-bold leading-9 tracking-tight text-gray-900">
          ลงทะเบียนเข้าใช้งาน
        </h2>
      </div>

      <div class="mt-10 sm:mx-auto sm:w-full sm:max-w-sm">
        <form class="space-y-6" @submit.prevent="handleRegister">
          <div>
            <label for="name" class="block text-sm font-medium leading-6 text-gray-900">
              ชื่อ-นามสกุล
            </label>
            <div class="mt-2">
              <input
                id="name"
                v-model="form.name"
                type="text"
                required
                class="block p-2 w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
              />
            </div>
          </div>

          <div>
            <label for="email" class="block text-sm font-medium leading-6 text-gray-900">
              อีเมล
            </label>
            <div class="mt-2">
              <input
                id="email"
                v-model="form.email"
                type="email"
                required
                class="block p-2 w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
              />
            </div>
          </div>

          <div>
            <label for="shares" class="block text-sm font-medium leading-6 text-gray-900">
              จำนวนหุ้นที่ถือ
            </label>
            <div class="mt-2">
              <input
                id="shares"
                v-model="form.shares"
                type="number"
                min="0"
                required
                class="block p-2 w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
              />
            </div>
          </div>

          <div>
            <label for="password" class="block text-sm font-medium leading-6 text-gray-900">
              รหัสผ่าน
            </label>
            <div class="mt-2">
              <input
                id="password"
                v-model="form.password"
                type="password"
                required
                class="block p-2 w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
              />
            </div>
          </div>

          <div>
            <label for="confirmPassword" class="block text-sm font-medium leading-6 text-gray-900">
              ยืนยันรหัสผ่าน
            </label>
            <div class="mt-2">
              <input
                id="confirmPassword"
                v-model="form.confirmPassword"
                type="password"
                required
                class="block p-2 w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
              />
            </div>
          </div>

          <div>
            <button
              type="submit"
              class="flex w-full justify-center rounded-md bg-indigo-600 px-3 py-1.5 text-sm font-semibold leading-6 text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
            >
              ลงทะเบียน
            </button>
          </div>
        </form>

        <p class="mt-10 text-center text-sm text-gray-500">
          มีบัญชีอยู่แล้ว?
          <NuxtLink to="/login" class="font-semibold leading-6 text-indigo-600 hover:text-indigo-500">
            เข้าสู่ระบบ
          </NuxtLink>
        </p>
      </div>
    </div>
  </div>
</template>

<script setup>
/* import { ref } from 'vue'
import { navigateTo } from '#app'
 */
const form = ref({
  name: '',
  email: '',
  shares: 0,
  password: '',
  confirmPassword: ''
})

async function handleRegister() {
  if (form.value.password !== form.value.confirmPassword) {
    alert('รหัสผ่านไม่ตรงกัน กรุณาตรวจสอบอีกครั้ง')
    return
  }

  try {
    // TODO: Implement registration logic here
    console.log('Form submitted:', form.value)
    // Redirect to login page after successful registration
    await navigateTo('/login')
  } catch (error) {
    console.error('Registration error:', error)
    alert('เกิดข้อผิดพลาดในการลงทะเบียน กรุณาลองใหม่อีกครั้ง')
  }
}
</script>