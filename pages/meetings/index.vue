<template>
  <div class="h-screen bg-white">
    <div class="px-4 sm:px-6 lg:px-8">
      <div class="sm:flex sm:items-center">
        <div class="sm:flex-auto">
          <h1 class="text-2xl font-semibold leading-6 text-gray-900">การประชุมทั้งหมด</h1>
          <p class="mt-2 text-sm text-gray-700">
            รายการประชุมผู้ถือหุ้นทั้งหมด ทั้งที่กำลังจะมาถึง กำลังดำเนินการ และเสร็จสิ้นแล้ว
          </p>
        </div>
      </div>
      <div class="mt-8 flow-root">
        <div class="-mx-4 -my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
          <div class="inline-block min-w-full py-2 align-middle sm:px-6 lg:px-8">
            <div class="overflow-hidden shadow ring-1 ring-black ring-opacity-5 sm:rounded-lg">
              <table class="min-w-full divide-y divide-gray-300">
                <thead class="bg-gray-50">
                  <tr>
                    <th scope="col" class="py-3.5 pl-4 pr-3 text-left text-sm font-semibold text-gray-900 sm:pl-6">
                      ชื่อการประชุม
                    </th>
                    <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">
                      วันที่
                    </th>
                    <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">
                      สถานะ
                    </th>
                    <th scope="col" class="relative py-3.5 pl-3 pr-4 sm:pr-6">
                      <span class="sr-only">Actions</span>
                    </th>
                  </tr>
                </thead>
                <tbody class="divide-y divide-gray-200 bg-white">
                  <tr v-for="meeting in meetings" :key="meeting.id">
                    <td class="whitespace-nowrap py-4 pl-4 pr-3 text-sm font-medium text-gray-900 sm:pl-6">
                      {{ meeting.title }}
                    </td>
                    <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                      {{ formatDate(meeting.startDate) }}
                    </td>
                    <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                      <span :class="getStatusClass(meeting.status)" class="inline-flex items-center rounded-md px-2 py-1 text-xs font-medium ring-1 ring-inset">
                        {{ getStatusText(meeting.status) }}
                      </span>
                    </td>
                    <td class="relative whitespace-nowrap py-4 pl-3 pr-4 text-right text-sm font-medium sm:pr-6">
                      <NuxtLink :to="'/meetings/' + meeting.id" class="text-indigo-600 hover:text-indigo-900">
                        เข้าร่วม<span class="sr-only">, {{ meeting.title }}</span>
                      </NuxtLink>
                    </td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const meetings = ref([
  {
    id: '1',
    title: 'การประชุมสามัญผู้ถือหุ้นประจำปี 2567',
    startDate: '2025-05-15T09:00:00',
    status: 'UPCOMING'
  },
  {
    id: '2',
    title: 'การประชุมวิสามัญผู้ถือหุ้น ครั้งที่ 1/2567',
    startDate: '2025-06-30T13:30:00',
    status: 'ONGOING'
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

function getStatusClass(status) {
  switch (status) {
    case 'UPCOMING':
      return 'bg-blue-50 text-blue-700 ring-blue-600/20'
    case 'ONGOING':
      return 'bg-green-50 text-green-700 ring-green-600/20'
    case 'COMPLETED':
      return 'bg-gray-50 text-gray-700 ring-gray-600/20'
    case 'CANCELLED':
      return 'bg-red-50 text-red-700 ring-red-600/20'
    default:
      return 'bg-gray-50 text-gray-700 ring-gray-600/20'
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
