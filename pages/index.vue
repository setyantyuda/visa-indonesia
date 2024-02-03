<template>
    <div class="overflow-y-auto bg-white rounded-tl-3xl w-full px-10 py-12 mt-7">
        <div class="font-bold text-3xl">Welcome back, Administrator!</div>
        <div class="text-secondary">Track, manage and forecast your platform informative here.</div>
        <div class="space-y-6 mt-8">
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
                    <input class="outline-none" placeholder="type here..."/>
                </div>
            </div>

            <div class="mt-5">
                <div
                    class="mt-5 overflow-x-auto rounded-md border bg-background scrollbar-thin scrollbar-thumb-input scrollbar-thumb-rounded-md"
                >
                    <table class="w-full border-1.5">
                        <thead>
                            <tr class="border-b text-left text-xs">
                                <th class="p-4 font-medium uppercase">Company</th>
                                <th class="p-4 font-medium uppercase">License use</th>
                                <th class="p-4 font-medium uppercase">Status</th>
                                <th class="p-4 font-medium uppercase">User</th>
                                <th class="p-4 font-medium uppercase">About</th>
                                <th class="p-4 font-medium uppercase"></th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr v-for="item in companyData" class="border-b hover:bg-slate-100 text-left text-sm last:border-b-0 hover:bg-muted">
                                <td class="p-4 flex space-x-5">
                                    <img src="/favicon.ico" alt="" class="rounded-full w-8 h-8 object-cover" />
                                    <div>
                                        <div class="font-medium">
                                            {{ item.name }}
                                        </div>
                                        <div>
                                            {{ item.site }}
                                        </div>
                                    </div>
                                </td>
                                <td class="p-4">
                                    <div class="w-full bg-gray-200 rounded-full h-2.5">
                                        <div class="bg-slate-600 h-2.5 rounded-full w-[50%]"></div>
                                    </div>
                                </td>
                                <td class="p-4">
                                    <span :class="getStatusClass(item.status)">
                                        {{ item.status }}
                                    </span>
                                </td>
                                <td class="p-4 flex -space-x-2">
                                    <div v-for="i in item.user">
                                        <img src="/administrator.jpg" class="w-6 h-6 object-cover rounded-full border-2 border-white hover:scale-150" alt="" />
                                    </div>
                                </td>
                                <td class="p-4">
                                    <div class="font-medium">{{ item?.about?.[0]?.title }}</div>
                                    <div>{{ item?.about?.[0]?.desc }}</div>
                                </td>
                                <td class="p-4 flex space-x-8">
                                    <Icon name="heroicons:pencil" class="h-6 w-6" />
                                    <Icon name="heroicons:trash" class="h-6 w-6" />
                                </td>
                            </tr>   
                        </tbody>
                    </table>
                    <div class="flex justify-between w-full">
                        <div class="p-4 font-medium text-secondary my-auto">
                            Page 1 of 10
                        </div>
                        <div class="p-4 flex">
                            <div class="border hover:bg-slate-100 rounded-l-md w-9 h-9 text-center flex justify-center">
                                <Icon name="heroicons:arrow-left" class="h-6 w-6 my-auto" />
                            </div>
                            <template v-for="(item, index) in pageLength">
                                <div
                                    :key="index"
                                    v-if="shouldRenderComponent(index, pageLength)"
                                    class="border hover:bg-slate-100 w-9 h-9 font-medium text-center flex justify-center"
                                >
                                    <div class="my-auto">
                                        {{ item }}
                                    </div>
                                </div>
                                <div
                                    v-else-if="index === Math.floor(pageLength / 2)"
                                    class="border hover:bg-slate-100 w-9 h-9 font-medium text-center flex justify-center"
                                >
                                    <div class="my-auto">
                                        ...
                                    </div>
                                </div>
                            </template>
                            <div class="border hover:bg-slate-100 rounded-r-md w-9 h-9 text-center flex justify-center">
                                <Icon name="heroicons:arrow-right" class="h-6 w-6 my-auto" />
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup lang="ts">
    const pageLength = 15
    const getStatusClass = (status: any) => {
        if (status === 'customer') {
            return 'bg-green-200/60 rounded-lg py-0.5 px-4 font-medium capitalize';
        } else if (status === 'chruned') {
            return 'bg-slate-300/60 rounded-lg py-0.5 px-4 font-medium capitalize';
        } else {
            return '';
        }
    };

    const shouldRenderComponent = (index: any, length: any) => {
      return index < 3 || index >= length - 3;
    };

    const companyData = [
        {
            id: 1,
            name: "Catalog",
            site: "catalogapp.io",
            license: 50,
            status: "customer",
            user: [
                {
                    name: "john",
                },
                {
                    name: "Alex",
                },
                {
                    name: "Anna",
                },
            ],
            about: [
                {
                    title: "Content Curation App",
                    desc: "lorem ipsum"
                },
            ]
        },
        {
            id: 2,
            name: "Circooles",
            site: "getcircooles.com",
            license: 80,
            status: "chruned",
            user: [
                {
                    name: "john",
                },
                {
                    name: "Alex",
                },
                {
                    name: "Anna",
                },
            ],
            about: [
                {
                    title: "Content Curation App",
                    desc: "lorem ipsum"
                },
            ]
        },
        {
            id: 3,
            name: "Command+R",
            site: "catalogapp.io",
            license: 40,
            status: "customer",
            user: [
                {
                    name: "john",
                },
                {
                    name: "Alex",
                },
                {
                    name: "Anna",
                },
            ],
            about: [
                {
                    title: "Content Curation App",
                    desc: "lorem ipsum"
                },
            ]
        },
        {
            id: 4,
            name: "Hourglass",
            site: "hourglass.app",
            license: 20,
            status: "customer",
            user: [
                {
                    name: "john",
                },
                {
                    name: "Alex",
                },
                {
                    name: "Anna",
                },
            ],
            about: [
                {
                    title: "Content Curation App",
                    desc: "lorem ipsum"
                },
            ]
        },
        {
            id: 5,
            name: "Catalog",
            site: "catalogapp.io",
            license: 50,
            status: "customer",
            user: [
                {
                    name: "john",
                },
                {
                    name: "Alex",
                },
                {
                    name: "Anna",
                },
            ],
            about: [
                {
                    title: "Content Curation App",
                    desc: "lorem ipsum"
                },
            ]
        },
        {
            id: 6,
            name: "Circooles",
            site: "getcircooles.com",
            license: 80,
            status: "chruned",
            user: [
                {
                    name: "john",
                },
                {
                    name: "Alex",
                },
                {
                    name: "Anna",
                },
            ],
            about: [
                {
                    title: "Content Curation App",
                    desc: "lorem ipsum"
                },
            ]
        },
        {
            id: 7,
            name: "Command+R",
            site: "catalogapp.io",
            license: 40,
            status: "customer",
            user: [
                {
                    name: "john",
                },
                {
                    name: "Alex",
                },
                {
                    name: "Anna",
                },
            ],
            about: [
                {
                    title: "Content Curation App",
                    desc: "lorem ipsum"
                },
            ]
        },
        {
            id: 8,
            name: "Hourglass",
            site: "hourglass.app",
            license: 20,
            status: "customer",
            user: [
                {
                    name: "john",
                },
                {
                    name: "Alex",
                },
                {
                    name: "Anna",
                },
            ],
            about: [
                {
                    title: "Content Curation App",
                    desc: "lorem ipsum"
                },
            ]
        }
    ]
</script>