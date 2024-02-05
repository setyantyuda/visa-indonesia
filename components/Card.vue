<template>
    <div class="border-2 rounded-lg p-5 flex flex-col">
        <div class="flex justify-between">
            <div class="text-lg">{{ title }}</div>
            <img 
                :src="icon"
                class="bg-white w-12 h-12 object-cover"
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