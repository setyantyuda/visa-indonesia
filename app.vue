<template>
  <div class="bg-primary w-full relative md:flex h-screen overflow-hidden">
    <Sidebar 
      :handleShow="() => handleShow()" 
      :class="`${mobileNav === true ? 'left-0' : '-left-96' } md:sticky fixed transition-all duration-500 h-screen bg-primary md:w-[25%] blcok'`"
    />
    
    <!-- icon for show mobile navbar -->
    <div class="flex md:hidden px-4 py-3 mb-1">
      <img
        src="https://api.iconify.design/tabler:menu-2.svg?color=%23ffffff"
        alt=""
        class="h-8 w-8 border-2 rounded-full p-1"
        @click="() => handleShow()"
      />
    </div>

    <NuxtLayout>
      <NuxtPage />
    </NuxtLayout>
  </div>
</template>

<script setup lang="ts">
  useHead({
    title: 'Visa Indonesia',
  })

  // ignore warning to clean console.log
  console.warn = () => {};

  // mobile nav logic
  const mobileNav = ref(false)
  const handleShow = () => {
    mobileNav.value = !mobileNav.value
  }
</script>