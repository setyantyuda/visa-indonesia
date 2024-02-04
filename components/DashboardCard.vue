<template>
    <div class="grid grid-cols-3 justify-between gap-4">
        <div class="border-2 rounded-lg p-5">
            <div class="flex justify-between">
                <div class="font-semibold text-lg">Revenue in Percentage</div>
                <img 
                    src="https://api.iconify.design/iconamoon:menu-kebab-vertical-fill.svg?color=%23667184"
                    class="w-6 h-6 hover:cursor-pointer"
                    alt=""
                />
            </div>
            <div class="text-secondary font-semibold">
                <div class="flex space-x-1">
                    <img src="https://api.iconify.design/iconamoon:arrow-up-1-bold.svg?color=%2312c17c" alt="" />
                    <div class="text-[#12c17c]">40%</div> 
                    <div>vs last month</div>
                </div>
            </div>
        </div>
        <div class="border-2 rounded-lg p-5">
            <div class="flex justify-between">
                <div class="font-semibold text-lg">Total Order</div>
                <img 
                    src="/book.png"
                    class="bg-white w-12 h-12 object-cover"
                    alt=""
                />
            </div>
            <div class="font-bold text-3xl">400 Orders</div>
        </div>
        <div class="border-2 rounded-lg p-5">
            <div class="flex justify-between">
                <div class="font-semibold text-lg">Pending Customer</div>
                <img 
                    src="/email.png"
                    class="bg-white w-12 h-12 object-cover"
                    alt=""
                />
            </div>
            <div class="font-bold text-3xl">20 Customer</div>
        </div>
    </div>
</template>