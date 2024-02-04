<template>
    <div class="fixed z-50 w-full h-full items-center top-0 bottom-0 left-0 right-0 bg-slate-500/30 flex">
        <div class="absolute space-y-5 mx-auto left-0 right-0 shadow-2xl w-[600px] max-h-[500px] overflow-y-auto p-8 rounded-3xl bg-white">
            <div class="absolute top-5 right-5">
                <button class="h-6 w-6 my-auto" @click="toggleModal()">
                    <Icon name="heroicons:x-mark" class="h-6 w-6 my-auto" />
                </button>
            </div>
            <h3 class="font-semibold text-xl text-primary">{{ title }}</h3>
            <slot/>
        </div>
    </div>
</template>

<script>
    export default {
        props: ['toggleModal', 'title']
    }
</script>