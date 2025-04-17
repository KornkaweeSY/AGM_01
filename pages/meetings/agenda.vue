<script setup>

const agenda = ref([
    {
        id: 1,
        header: 'วาระที่ 1',
        title: 'พิจารณารับรองรายงานการประชุมสามัญผู้ถือหุ้น ประจำปี 2566',
        description: 'ข้อเท็จจริงและเหตุผล บริษัทได้จัดทำรายงานการประชุมสามัญผู้ถือหุ้น ประจำปี 2566 ซึ่งประชุมเมื่อวันที่ 25 เมษายน 2566 แล้วเสร็จภายใน 14 วัน นับแต่วันประชุมสามัญผู้ถือหุ้น และได้ส่งให้ตลาดหลักทรัพย์แห่งประเทศไทยและกระทรวงพาณิชย์ภายในระยะเวลาที่กฎหมายกำหนด พร้อมทั้งเผยแพร่ทางเว็บไซต์ของบริษัท',
        options: [
            { id: 1, label: 'อนุมัติ' },
            { id: 2, label: 'ไม่อนุมัติ' },
            { id: 3, label: 'งดออกเสียง' }
        ],
        total: 900000
    },
    {
        id: 2,
        header: 'วาระที่ 2',
        title: 'พิจารณาอนุมัติงบการเงินของบริษัท สำหรับรอบปีบัญชีสิ้นสุด ณ วันที่ 31 ธันวาคม 2566',
        description: 'ข้อเท็จจริงและเหตุผล บริษัทได้จัดทำงบการเงินของบริษัท สำหรับรอบปีบัญชีสิ้นสุด ณ วันที่ 31 ธันวาคม 2566 ซึ่งผ่านการตรวจสอบจากผู้สอบบัญชีรับอนุญาตแล้ว',
        options: [
            { id: 1, label: 'อนุมัติ' },
            { id: 2, label: 'ไม่อนุมัติ' },
            { id: 3, label: 'งดออกเสียง' }
        ],
        total: 900000
    }
])

const selectedValues = ref({})

const handleSubmit = () => {
    console.log('Selected values:', selectedValues.value)
}
</script>

<template>
    <div class="h-full bg-white">
        <div class="px-4 sm:px-6 lg:px-8">
            <form @submit.prevent="handleSubmit" class="flex flex-col justify-center items-center gap-4">
                <div v-for="item in agenda" :key="item.id"
                    class="w-[400px] flex flex-col justify-center items-start border border-gray-300 rounded-xl px-4 py-6 gap-4">
                    <h2 class="text-xl font-semibold">{{ item.header }}</h2>
                    <p class="text-gray-800">{{ item.title }}</p>
                    <p class="text-gray-800">{{ item.description }}</p>
                    <div class="flex flex-col justify-start items-start gap-2">
                        <div v-for="option in item.options" :key="option.id" class="flex items-center gap-2">
                            <input type="radio" 
                                :name="`agenda-${item.id}`"
                                :value="option.id"
                                :id="`agenda-${item.id}-${option.id}`"
                                v-model="selectedValues[item.id]" class="custom-radio" />
                            <label :for="`agenda-${item.id}-${option.id}`">{{ option.label }}</label>
                        </div>
                    </div>
                </div>
                <div class="flex justify-end items-center gap-2">
                    <button type="button" class="bg-gray-300 text-gray-700 px-4 py-2 rounded-md hover:bg-gray-400 transition-colors">ยกเลิก</button>
                    <button type="submit" class="bg-indigo-600 text-white px-4 py-2 rounded-md hover:bg-indigo-700 transition-colors">บันทึก</button>
                </div>
            </form>
        </div>
    </div>
</template>

<style>

</style>
