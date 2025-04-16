<template>
  <div class="bg-white">
    <div class="mx-auto max-w-7xl py-24 sm:px-6 sm:py-32 lg:px-8">
      <div class="relative isolate overflow-hidden bg-gray-900 px-6 py-24 shadow-2xl sm:rounded-3xl sm:px-24">
        <h2 class="mx-auto max-w-2xl text-center text-3xl font-bold tracking-tight text-white sm:text-4xl">
          ข้อมูลผู้ถือหุ้น
        </h2>
        
        <div class="mx-auto mt-10 max-w-xl space-y-8">
          <!-- Profile Information -->
          <div class="bg-white/5 p-6 rounded-lg">
            <h3 class="text-lg font-medium leading-6 text-white">ข้อมูลส่วนตัว</h3>
            <dl class="mt-5 grid grid-cols-1 gap-5 sm:grid-cols-2">
              <div class="overflow-hidden rounded-lg bg-white/5 px-4 py-5">
                <dt class="truncate text-sm font-medium text-gray-300">ชื่อ-นามสกุล</dt>
                <dd class="mt-1 text-lg font-semibold tracking-tight text-white">{{ user.name }}</dd>
              </div>
              <div class="overflow-hidden rounded-lg bg-white/5 px-4 py-5">
                <dt class="truncate text-sm font-medium text-gray-300">อีเมล</dt>
                <dd class="mt-1 text-lg font-semibold tracking-tight text-white">{{ user.email }}</dd>
              </div>
              <div class="overflow-hidden rounded-lg bg-white/5 px-4 py-5">
                <dt class="truncate text-sm font-medium text-gray-300">จำนวนหุ้น</dt>
                <dd class="mt-1 text-lg font-semibold tracking-tight text-white">{{ user.shares.toLocaleString() }} หุ้น</dd>
              </div>
              <div class="overflow-hidden rounded-lg bg-white/5 px-4 py-5">
                <dt class="truncate text-sm font-medium text-gray-300">สถานะ</dt>
                <dd class="mt-1">
                  <span class="inline-flex items-center rounded-md bg-green-400/10 px-2 py-1 text-xs font-medium text-green-400 ring-1 ring-inset ring-green-400/20">
                    {{ getRoleText(user.role) }}
                  </span>
                </dd>
              </div>
            </dl>
          </div>

          <!-- Recent Meetings -->
          <div class="bg-white/5 p-6 rounded-lg">
            <h3 class="text-lg font-medium leading-6 text-white">การประชุมล่าสุด</h3>
            <ul role="list" class="mt-6 divide-y divide-white/5">
              <li v-for="meeting in recentMeetings" :key="meeting.id" class="py-4">
                <div class="flex items-center gap-x-3">
                  <h4 class="flex-auto truncate text-sm font-semibold leading-6 text-white">{{ meeting.title }}</h4>
                  <time :datetime="meeting.date" class="flex-none text-xs text-gray-400">{{ formatDate(meeting.date) }}</time>
                </div>
                <p class="mt-3 truncate text-sm text-gray-400">
                  สถานะ: {{ getStatusText(meeting.status) }}
                </p>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
// Mock user data
const user = ref({
  name: 'คุณสมชาย ใจดี',
  email: 'somchai@gamil.com',
  shares: 10000,
  role: 'SHAREHOLDER'
})

// Mock recent meetings
const recentMeetings = ref([
  {
    id: 1,
    title: 'การประชุมสามัญผู้ถือหุ้นประจำปี 2567',
    date: '2025-05-15T09:00:00',
    status: 'UPCOMING'
  },
  {
    id: 2,
    title: 'การประชุมวิสามัญผู้ถือหุ้น ครั้งที่ 1/2566',
    date: '2024-12-15T13:30:00',
    status: 'COMPLETED'
  }
])

function formatDate(dateString) {
  const options = {
    year: 'numeric',
    month: 'long',
    day: 'numeric',
    hour: '2-digit',
    minute: '2-digit'
  }
  return new Date(dateString).toLocaleDateString('th-TH', options)
}

function getRoleText(role) {
  switch (role) {
    case 'ADMIN':
      return 'ผู้ดูแลระบบ'
    case 'MODERATOR':
      return 'ผู้ดำเนินการประชุม'
    case 'SHAREHOLDER':
      return 'ผู้ถือหุ้น'
    default:
      return role
  }
}

function getStatusText(status) {
  switch (status) {
    case 'UPCOMING':
      return 'กำลังจะมาถึง'
    case 'ONGOING':
      return 'กำลังดำเนินการ'
    case 'COMPLETED':
      return 'เสร็จสิ้น'
    case 'CANCELLED':
      return 'ยกเลิก'
    default:
      return status
  }
}
</script>
