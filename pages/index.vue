<template>
    <div class="bg-white rounded-tl-3xl w-full px-10 pt-12 mt-5">
        <div class="font-bold text-3xl">Welcome back, Administrator!</div>
        <div class="text-secondary">Track, manage and forecast your platform informative here.</div>
        <div class="space-y-6 mt-8">
            <div class="grid grid-cols-3 justify-between gap-4">
                <div class="border-2 rounded-md p-5">
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
                <div class="border-2 rounded-md p-5">
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
                <div class="border-2 rounded-md p-5">
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

            <div class="grid grid-cols-3 gap-5">
                <div></div>
                <div></div>
                <div class="border-2 rounded-md p-2 flex space-x-3">
                    <img 
                        src="https://api.iconify.design/iconamoon:search-bold.svg?color=%23667184"
                        class="w-6 h-6 object-cover"
                        alt=""
                    />
                    <span class="text-secondary border-r-2 pr-3">Search</span>
                    <input class="outline-none"/>
                </div>
            </div>

            <div class="mt-5">
                <div
                    class="mt-5 overflow-x-auto rounded-md border bg-background scrollbar-thin scrollbar-thumb-input scrollbar-thumb-rounded-md"
                >
                    <table class="w-full border-collapse">
                        <thead>
                            <tr class="border-b text-left text-xs">
                                <th class="p-4 font-medium uppercase text-muted-foreground">Product</th>
                                <th class="p-4 font-medium uppercase text-muted-foreground">Payment</th>
                                <th class="p-4 font-medium uppercase text-muted-foreground">Status</th>
                                <th class="p-4 font-medium uppercase text-muted-foreground"></th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr v-for="n in 6" class="border-b text-left text-sm last:border-b-0 hover:bg-muted">
                                <td class="p-4">Apple Watch</td>
                                <td class="p-4">Paid</td>
                                <td class="p-4">Submit</td>
                                <td class="p-4">
                                <div class="flex items-center gap-3">
                                    <button>
                                    <Icon name="heroicons:pencil" class="h-4 w-4 text-muted-foreground" />
                                    </button>
                                </div>
                                </td>
                            </tr>   
                        </tbody>
                    </table>
                </div>
            </div>
        </div>
    </div>
</template>