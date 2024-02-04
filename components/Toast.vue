<template>
    <div 
        :class="{ 
            'bottom-4 -right-96': !open, 
            'bottom-4 right-10': open, 
            'fixed transition-all bg-blue-600 duration-300 capitalize space-x-5 rounded-xl text-white z-50 px-8 py-2 flex': true
        }">
        <div class="my-auto font-medium">
            {{ text }} data selected
        </div>
        <button class="" @click="close()">
            <Icon name="heroicons:x-mark" class="h-7 w-7 object-cover" />
        </button>
    </div>
</template>

<script>
    export default {
        props: ['open', 'close', 'text']
    }
</script>