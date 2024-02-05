<template>
  <div class="bg-primary h-full lg:h-screen lg:flex">
    <Sidebar 
      :handleShow="() => handleShow()" 
      :class="`${mobileNav === true ? 'left-0' : '-left-96' } lg:sticky z-50 lg:w-full fixed transition-all duration-500 h-full bg-primary lg:w-[25%]'`"
    />
    
    <!-- icon for show mobile navbar -->
    <div class="sticky z-40 flex lg:hidden px-4 py-3">
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