<template>
    <div class="border-2 rounded-lg p-5 flex flex-col">
        <div class="flex justify-between">
            <div class="text-lg">{{ title }}</div>
            <img 
                :src="icon"
                class="bg-white md:w-12 md:h-12 w-20 h-20 object-cover"
                alt=""
            />
        </div>
        <slot/>
    </div>
</template>

<script>
    export default {
        props: ['title', 'icon']
    }
</script>