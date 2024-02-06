<template>
    <div class="md:flex justify-between w-full">
        <div class="pt-4 text-secondary my-auto lg:text-left text-center">
            Page {{ currentPage }} of {{ totalPage }}
        </div>
        <div class="p-4 flex">
            <!-- left arrow -->
            <div @click="() => changePageHandler(currentPage - 1, totalPage)" :disabled="currentPage === 1" class="border hover:bg-slate-200 hover:cursor-pointer rounded-l-md w-9 h-9 text-center flex justify-center" :class="{ 'opacity-50': currentPage === 1 }">
                <Icon name="heroicons:arrow-left" class="h-6 w-6 my-auto" />
            </div>

            <!-- show the first page -->
            <template v-if="showFirstPage">
                <div @click="() => changePageHandler(1, totalPage)" class="border hover:bg-slate-200 hover:cursor-pointer w-9 h-9 text-center flex justify-center">
                    <div class="my-auto">1</div>
                </div>
            </template>

            <!-- unrendred page -->
            <div v-if="showEllipsisBefore && totalPage > 1" class="border w-9 h-9 text-center flex justify-center">
                <div class="my-auto">...</div>
            </div>

            <!-- list page -->
            <template v-if="totalPage > 1" v-for="item in paginatedItems" :key="item">
                <div
                    @click="() => changePageHandler(item, totalPage)"
                    class="border hover:bg-slate-200 hover:cursor-pointer w-9 h-9 text-center flex justify-center"
                    :class="{ 'bg-slate-200': item === currentPage }"
                >
                    <div class="my-auto">{{ item }}</div>
                </div>
            </template>

            <!-- unrendred page -->
            <div v-if="showEllipsisAfter && totalPage > 5" class="border w-9 h-9 text-center flex justify-center">
                <div class="my-auto">...</div>
            </div>

            <!-- show the last page -->
            <template v-if="showLastPage && totalPage > 5">
                <div @click="() => changePageHandler(totalPage, totalPage)" class="border hover:bg-slate-200 hover:cursor-pointer w-9 h-9 text-center flex justify-center">
                    <div class="my-auto">{{ totalPage }}</div>
                </div>
            </template>

            <!-- right arrow -->
            <div @click="() => changePageHandler(currentPage + 1, totalPage)" :disabled="currentPage === totalPage" class="border hover:bg-slate-200 hover:cursor-pointer rounded-r-md w-9 h-9 text-center flex justify-center" :class="{ 'opacity-50': currentPage === totalPage }">
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

    // generate list of page by the available total page
    const generatePaginatedItems = (current: any, total: any) => {
        console.log("bayu", total)
        const visiblePages = total >= 5 ? 5 : total
        const middleIndex = Math.floor(visiblePages / 2);
        const start = Math.min(Math.max(1, current - middleIndex), total - visiblePages + 1);
        const end = Math.min(start + visiblePages - 1, total);
        const result = [];
        for (let i = start; i <= end; i++) {
            result.push(i);
        }

        return result;
    };

    // show default page list when page not change
    const defaultPagination = computed(() => {
        return generatePaginatedItems(currentPage, totalPage);
    });
    paginatedItems.value = defaultPagination.value;
    
    // handler for changing page
    const changePageHandler = (page: any, total: any) => {
        changePage(page);
        paginatedItems.value = generatePaginatedItems(page, total);
    };
    
    // logic for showing icon for unrendered page, first page, and last page
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