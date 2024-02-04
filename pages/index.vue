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
                                <th class="p-4 font-medium uppercase">Company<span><Icon name="heroicons:arrow-up" class="h-4 w-4 ml-2 hover:rotate-180 transition-all duration-200 bg-slate-300 rounded-full p-0.5" /></span></th>
                                <th class="p-4 font-medium uppercase">License use<span><Icon name="heroicons:arrow-up" class="h-4 w-4 ml-2 hover:rotate-180 transition-all duration-200 bg-slate-300 rounded-full p-0.5" /></span></th>
                                <th class="p-4 font-medium uppercase">Status<span><Icon name="heroicons:arrow-up" class="h-4 w-4 ml-2 hover:rotate-180 transition-all duration-200 bg-slate-300 rounded-full p-0.5" /></span></th>
                                <th class="p-4 font-medium uppercase">User<span><Icon name="heroicons:arrow-up" class="h-4 w-4 ml-2 hover:rotate-180 transition-all duration-200 bg-slate-300 rounded-full p-0.5" /></span></th>
                                <th class="p-4 font-medium uppercase">About<span><Icon name="heroicons:arrow-up" class="h-4 w-4 ml-2 hover:rotate-180 transition-all duration-200 bg-slate-300 rounded-full p-0.5" /></span></th>
                                <th class="p-4 font-medium uppercase"></th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr v-for="item in paginatedData" class="border-b hover:bg-slate-100 text-left text-sm last:border-b-0 hover:bg-muted">
                                <td class="p-4 flex space-x-5">
                                    <img :src="item.image" alt="" class="rounded-full w-10 h-10 hover:scale-150 shadow-none transition-all duration-300 object-cover" />
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
                                    <template v-for="(i, index) in item.user">
                                        <div 
                                            v-if="shouldRenderUserComponent(index)"
                                            @click="() => toggleModal('openModalUser')"
                                        >
                                            <img 
                                                :key="index" 
                                                :src="i.image"
                                                class="hover:cursor-pointer w-6 h-6 object-cover rounded-full border-2 border-white hover:scale-150" 
                                                alt=""
                                            />
                                        </div>
                                        <div
                                            v-else-if="index === item.user.length - 1"
                                            @click="() => toggleModal('openModalUser')"
                                        > 
                                            <div :key="index" class="hover:cursor-pointer w-6 h-6 p-[1px] text-xs font-medium overflow-hidden object-cover rounded-full border-2 bg-slate-200 border-white hover:scale-150" >
                                                +{{index + 1 - maxRenderedUser}}
                                            </div>
                                        </div>
                                    </template>
                                </td>
                                <td class="p-4 max-w-[350px]">
                                    <div class="font-medium">{{ item?.about?.[0]?.title }}</div>
                                    <div class="overflow-hidden">{{ item?.about?.[0]?.desc }}</div>
                                </td>
                                <td class="p-4 flex space-x-8">
                                    <Icon @click="toggleModal('openModalEdit')" name="heroicons:pencil" class="h-6 w-6 hover:cursor-pointer" />
                                    <Icon @click="toggleModal('openModalDelete')" name="heroicons:trash" class="h-6 w-6 hover:cursor-pointer" />
                                </td>
                            </tr>   
                        </tbody>
                    </table>
                    <div class="flex justify-between w-full">
                        <div class="p-4 font-medium text-secondary my-auto">
                            Page {{ currentPage }} of {{ totalPage }}
                        </div>
                        <div class="p-4 flex">
                            <div @click="changePage(currentPage - 1)" class="border hover:bg-slate-200 hover:cursor-pointer rounded-l-md w-9 h-9 text-center flex justify-center">
                                <Icon name="heroicons:arrow-left" class="h-6 w-6 my-auto" />
                            </div>
                            <template v-for="(item, index) in totalPage">
                                <div
                                    :key="index"
                                    @click="changePage(item)"
                                    v-if="shouldRenderComponent(index, totalPage)"
                                    class="border hover:bg-slate-200 hover:cursor-pointer w-9 h-9 font-medium text-center flex justify-center"
                                >
                                    <div class="my-auto">
                                        {{ item }}
                                    </div>
                                </div>
                                <div
                                    v-else-if="index === Math.floor(totalPage / 2)"
                                    class="border hover:bg-slate-200 w-9 h-9 font-medium text-center flex justify-center"
                                >
                                    <div class="my-auto">
                                        ...
                                    </div>
                                </div>
                            </template>
                            <div @click="changePage(currentPage + 1)" class="border hover:bg-slate-200 hover:cursor-pointer rounded-r-md w-9 h-9 text-center flex justify-center">
                                <Icon name="heroicons:arrow-right" class="h-6 w-6 my-auto" />
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
    <Popup 
        v-if="modalTrigger.openModalUser" 
        :toggleModal="() => toggleModal('openModalUser')"
        title="Company User List"
    >
        <h1>Popup</h1>
    </Popup>
    <Popup 
        v-if="modalTrigger.openModalEdit" 
        :toggleModal="() => toggleModal('openModalEdit')"
        title="Edit Company Detail"
    >
        <h1>Popup</h1>
    </Popup>
    <Popup 
        v-if="modalTrigger.openModalDelete" 
        :toggleModal="() => toggleModal('openModalDelete')"
        title="Delete Company"
    >
        <h1>Popup</h1>
    </Popup>
</template>

<script setup lang="ts">
    const generateRandomName = () => {
        const names = ['John', 'Jane', 'Alex', 'Anna', 'Bob', 'Charlie', 'David', 'Emma', 'Frank', 'Grace'];
        return names[Math.floor(Math.random() * names.length)];
    };

    const generateRandomImage = () => {
        const placeholderImages = [
            'https://placekitten.com/50/50',
            'https://placebear.com/50/50',
            'https://placekitten.com/60/60',
            'https://placebear.com/60/60',
            '/administrator.jpg',
        ];
        return placeholderImages[Math.floor(Math.random() * placeholderImages.length)];
    };

    const generateDummyData = () => {
        const companyData = [];

        for (let i = 1; i <= 100; i++) {
            // dibuat minimal 5 user di tiap company
            const numberOfUsers = Math.max(5, Math.floor(Math.random() * 10) + 1);

            const newCompany = {
                id: i,
                name: `Company${i}`,
                image: generateRandomImage(),
                site: `company${i}.com`,
                license: Math.floor(Math.random() * 100) + 1,
                status: i % 2 === 0 ? 'churned' : 'customer',
                user: Array.from({ length: numberOfUsers }, (_, index) => ({
                    name: generateRandomName(),
                    image: generateRandomImage(),
                })),
                about: [
                {
                    title: 'Lorem Ipsum Title',
                    desc: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.',
                },
                ],
            };

            companyData.push(newCompany);
            }

            return companyData;
    };
    const companyData = generateDummyData();

    const modalTrigger = ref({
        openModalUser: false,
        openModalEdit: false,
        openModalDelete: false
    })
    const toggleModal = (e: boolean) => {
        modalTrigger.value[e] = !modalTrigger.value[e]
    }

    const currentPage = ref(1);
    const pageSize = 10
    const totalPage = companyData.length / pageSize
    const paginatedData = computed(() => {
        const startIndex = (currentPage.value - 1) * pageSize;
        const endIndex = startIndex + pageSize;

        return companyData.slice(startIndex, endIndex);
    });

    const changePage = (page: any) => {
        if ( page === 0) {
            currentPage.value = 1
        } else if (page === totalPage + 1) {
            currentPage.value === totalPage
        } else {
            currentPage.value = page
        }
    }

    const getStatusClass = (status: any) => {
        if (status === 'customer') {
            return 'bg-green-200/60 rounded-lg py-0.5 px-4 font-medium capitalize';
        } else if (status === 'churned') {
            return 'bg-slate-300/60 rounded-lg py-0.5 px-4 font-medium capitalize';
        } else {
            return '';
        }
    };

    const shouldRenderComponent = (index: any, length: any) => {
      return index < 3 || index >= length - 3;
    };

    const maxRenderedUser = 5
    const shouldRenderUserComponent = (index: any) => {
      return index < maxRenderedUser;
    };
</script>