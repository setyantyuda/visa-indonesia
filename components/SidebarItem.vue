<template>
    <div class="flex flex-col">
      <template v-for="(item, i) in props.links" :key="i">
        <NuxtLink
            v-if="!item.items"
            to="#"
            class="inline-flex items-center gap-4 p-3 px-4 text-left text-[15px] bg-primary hover:bg-[#344155] rounded-md"
        >
            <img :src="item.icon" alt="" class="w-5 h-5" />
            <p class="truncate">
                {{ item.title }}
            </p>
        </NuxtLink>
      </template>
    </div>
</template>

<script setup lang="ts">
    const props = defineProps<{
        links?: any[];
    }>();
</script>
  