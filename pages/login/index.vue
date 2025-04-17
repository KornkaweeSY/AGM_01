<template>
    <div class="min-h-full bg-white flex flex-col justify-center items-center">
        <div class="w-[400px] px-6 py-12 lg:px-8 border rounded-md">
            <div class="sm:mx-auto sm:w-full sm:max-w-md">
                <h2 class="text-center text-3xl font-bold tracking-tight text-gray-900">เข้าสู่ระบบ</h2>
            </div>

            <div class="mt-8 sm:mx-auto sm:w-full sm:max-w-md">
                <div class="bg-white py-8 px-4 shadow sm:rounded-lg sm:px-10">
                    <form class="space-y-6" @submit.prevent="handleLogin">
                        <div>
                            <label for="email" class="block text-sm font-medium text-gray-700">อีเมล</label>
                            <div class="mt-1">
                                <input id="email" v-model="email" name="email" type="email" required
                                    class="block w-full appearance-none rounded-md border border-gray-300 px-3 py-2 placeholder-gray-400 shadow-sm focus:border-indigo-500 focus:outline-none focus:ring-indigo-500 sm:text-sm" />
                            </div>
                        </div>

                        <div>
                            <label for="password" class="block text-sm font-medium text-gray-700">รหัสผ่าน</label>
                            <div class="mt-1">
                                <input id="password" v-model="password" name="password" type="password" required
                                    class="block w-full appearance-none rounded-md border border-gray-300 px-3 py-2 placeholder-gray-400 shadow-sm focus:border-indigo-500 focus:outline-none focus:ring-indigo-500 sm:text-sm" />
                            </div>
                        </div>

                        <div>
                            <button type="submit"
                                class="flex w-full justify-center rounded-md border border-transparent bg-indigo-600 py-2 px-4 text-sm font-medium text-white shadow-sm hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2">
                                เข้าสู่ระบบ
                            </button>
                        </div>
                    </form>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()
const email = ref('')
const password = ref('')

const handleLogin = async () => {
    try {
        // TODO: Implement actual login logic here
        console.log('Login attempt with:', { email: email.value, password: password.value })
        // For now, just redirect to home page
        router.push('/')
    } catch (error) {
        console.error('Login failed:', error)
    }
}
</script>