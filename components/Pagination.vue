<template>
    <div class="flex justify-between w-full">
        <div class="p-4 text-secondary my-auto">
            Page {{ currentPage }} of {{ totalPage }}
        </div>
        <div class="p-4 flex">
            <div @click="() => changePageHandler(currentPage - 1)" :disabled="currentPage === 1" class="border hover:bg-slate-200 hover:cursor-pointer rounded-l-md w-9 h-9 text-center flex justify-center" :class="{ 'opacity-50': currentPage === 1 }">
                <Icon name="heroicons:arrow-left" class="h-6 w-6 my-auto" />
            </div>

            <template v-if="showFirstPage">
                <div @click="() => changePageHandler(1)" class="border hover:bg-slate-200 hover:cursor-pointer w-9 h-9 text-center flex justify-center">
                    <div class="my-auto">1</div>
                </div>
            </template>

            <div v-if="showEllipsisBefore" class="border w-9 h-9 text-center flex justify-center">
                <div class="my-auto">...</div>
            </div>

            <template v-for="item in paginatedItems" :key="item">
                <div
                    @click="() => changePageHandler(item)"
                    class="border hover:bg-slate-200 hover:cursor-pointer w-9 h-9 text-center flex justify-center"
                    :class="{ 'bg-slate-200': item === currentPage }"
                >
                    <div class="my-auto">{{ item }}</div>
                </div>
            </template>

            <div v-if="showEllipsisAfter" class="border w-9 h-9 text-center flex justify-center">
                <div class="my-auto">...</div>
            </div>

            <template v-if="showLastPage">
                <div @click="() => changePageHandler(totalPage)" class="border hover:bg-slate-200 hover:cursor-pointer w-9 h-9 text-center flex justify-center">
                    <div class="my-auto">{{ totalPage }}</div>
                </div>
            </template>

            <div @click="() => changePageHandler(currentPage + 1)" :disabled="currentPage === totalPage" class="border hover:bg-slate-200 hover:cursor-pointer rounded-r-md w-9 h-9 text-center flex justify-center" :class="{ 'opacity-50': currentPage === totalPage }">
                <Icon name="heroicons:arrow-right" class="h-6 w-6 my-auto" />
            </div>
        </div>
    </div>
</template>

<script setup lang="ts">
    const {currentPage, totalPage, changePage} = defineProps<{
        currentPage?: any,
        totalPage?: any,
        changePage?: any
    }>();
    
    const paginatedItems = ref<number[]>([])
    const visiblePages = 5;

    const generatePaginatedItems = (current: any, total: any) => {
    const middleIndex = Math.floor(visiblePages / 2);
    const start = Math.min(Math.max(1, current - middleIndex), total - visiblePages + 1);
    const end = Math.min(start + visiblePages - 1, total);

    const result = [];
    for (let i = start; i <= end; i++) {
        result.push(i);
    }

    return result;
    };

    const defaultPagination = computed(() => {
        return generatePaginatedItems(currentPage, totalPage);
    });
    paginatedItems.value = defaultPagination.value;

    const changePageHandler = (page: any) => {
        changePage(page);
        paginatedItems.value = generatePaginatedItems(page, totalPage);
    };
    
    const showEllipsisBefore = computed(() => {
        return paginatedItems.value[0] > 2;
    });

    const showEllipsisAfter = computed(() => {
        return paginatedItems.value[paginatedItems.value.length - 1] < totalPage - 1;
    });

    const showFirstPage = computed(() => {
        return paginatedItems.value[0] > 1;
    });

    const showLastPage = computed(() => {
        return paginatedItems.value[paginatedItems.value.length - 1] <= totalPage - 1;
    });

</script>