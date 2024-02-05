<template>
    <div class="md:grid grid-cols-3 md:space-y-0 space-y-3 justify-between gap-4">
        <div class="border-2 rounded-lg p-5">
            <div class="flex justify-between">
                <div class="text-lg">Revenue in Percentage</div>
                <div class="relative">
                    <img 
                        @click="toggleDropdown('openDropdown')"
                        src="https://api.iconify.design/iconamoon:menu-kebab-vertical-fill.svg?color=%23667184"
                        class="w-6 h-6 hover:cursor-pointer"
                        alt=""
                    />
                    <div v-if="dropdownTrigger.openDropdown" class="absolute top-0 right-0 w-[250px] capitalize bg-white border rounded-lg shadow-xl px-5 py-3 pr-10">
                        <div class="absolute top-1 right-2">
                            <button @click="toggleDropdown('openDropdown')" class="h-5 w-5 my-auto">
                                <Icon name="heroicons:x-mark" class="h-5 w-5 my-auto" />
                            </button>
                        </div>
                        <div @click="selected('year')" class="hover:bg-slate-200 px-2 py-1 text-sm cursor-pointer border-b-2">compare to last year</div>
                        <div @click="selected('month')" class="hover:bg-slate-200 px-2 py-1 text-sm cursor-pointer border-b-2">compare to last month</div>
                        <div @click="selected('week')" class="hover:bg-slate-200 px-2 py-1 text-sm cursor-pointer border-b-2">compare to last week</div>
                        <div @click="selected('day')" class="hover:bg-slate-200 px-2 py-1 text-sm cursor-pointer">compare to last day</div>
                    </div>
                </div>
            </div>
            <div class="flex justify-between">
                <div class="text-secondary flex flex-col">
                    <div class="flex-grow"></div>
                    <div class="flex space-x-1">
                        <img v-if="selectedData[0]?.type === 'increase'" src="https://api.iconify.design/iconamoon:arrow-up-1-bold.svg?color=%2312c17c" alt="" />
                        <img v-if="selectedData[0]?.type === 'decrease'" src="https://api.iconify.design/iconamoon:arrow-down-1-bold.svg?color=%23fd3581" alt="" />
                        <div :class="`${selectedData[0]?.type === 'increase' ? 'text-[#12c17c] font-semibold' : 'text-[#fd3581] font-semibold'}`">{{ selectedData[0]?.data }}</div> 
                        <div>vs last {{ selectedData[0]?.time }}</div>
                    </div>
                </div>
                <div class="">
                    <img :src="`${selectedData[0]?.type === 'increase' ? '/increase.png' : '/decrease.png'}`" alt="" class="w-24 h-24"/>
                </div>
            </div>
        </div>

        <Card 
            :title="'Total Order'" 
            :icon="'/book.png'"
        >
            <div class="flex-grow"></div>
            <div class="font-bold md:text-3xl text-xl">400 Orders</div>
        </Card>
        <Card 
            :title="'Pending Customer'" 
            :icon="'/email.png'"
        >
            <div class="flex-grow"></div>
            <div class="font-bold md:text-3xl text-xl">20 Customer</div>
        </Card>
    </div>
</template>

<script setup lang="ts">
    const dropdownTrigger = ref({
        openDropdown: false,
    })

    const dataChart = [
        {
            time: "year",
            data: "25%",
            type: "decrease"
        },
        {
            time: "month",
            data: "40%",
            type: "increase"
        },
        {
            time: "week",
            data: "30%",
            type: "increase"
        },
        {
            time: "day",
            data: "10%",
            type: "decrease"
        },
    ]

    let selectedData = [dataChart[1]]

    const selected = (data: any) => {
        const filteredData = dataChart.filter((item) => item.time === data )
        selectedData = filteredData
        toggleDropdown('openDropdown')
    } 

    const toggleDropdown = (e: any) => {
        dropdownTrigger.value[e] = !dropdownTrigger.value[e]
    }
</script>